# AlphaFold3の実行方法

以下の作業をfloyd上で行います。

### Input fileの準備

[AlphaFold3のリポジトリ](https://github.com/google-deepmind/alphafold3)に解説されているように、以下のようなjsonファイルを用意します。 `2pv7.json` とします。

```json
{
  "name": "2PV7",
  "sequences": [
    {
      "protein": {
        "id": ["A", "B"],
        "sequence": "GMRESYANENQFGFKTINSDIHKIVIVGGYGKLGGLFARYLRASGYPISILDREDWAVAESILANADVVIVSVPINLTLETIERLKPYLTENMLLADLTSVKREPLAKMLEVHTGAVLGLHPMFGADIASMAKQVVVRCDGRFPERYEWLLEQIQIWGAKIYQTNATEHDHNMTYIQALRHFSTFANGLHLSKQPINLANLLALSSPIYRLELAMIGRLFAQDAELYADIIMDKSENLAVIETLKQTYDEALTFFENNDRQGFIDAFHKVRDWFGDYSEQFLKESRQLLQQANDLKQG"
      }
    }
  ],
  "modelSeeds": [1],
  "dialect": "alphafold3",
  "version": 1
}
```

または、fastaからjsonへコンバートするツールを使うこともできます。ここでは、floydにインストールした `fasta2json.py` を使います。

fastaファイルを用意します。 `2pv7.fasta` とします。 `#2`はhomo-dimerを意味します。詳しくは [ツールの開発元](https://github.com/snufoodbiochem/Alphafold3_tools?tab=readme-ov-file) をご覧ください。

```fasta
>2PV7 #2
GMRESYANENQFGFKTINSDIHKIVIVGGYGKLGGLFARYLRASGYPISILDREDWAVAESILANADVVIVSVPINLTLETIERLKPYLTENMLLADLTSVKREPLAKMLEVHTGAVLGLHPMFGADIASMAKQVVVRCDGRFPERYEWLLEQIQIWGAKIYQTNATEHDHNMTYIQALRHFSTFANGLHLSKQPINLANLLALSSPIYRLELAMIGRLFAQDAELYADIIMDKSENLAVIETLKQTYDEALTFFENNDRQGFIDAFHKVRDWFGDYSEQFLKESRQLLQQANDLKQG
```

以下でjsonファイルへコンバートします。PATHは通っています。これで `2pv7.json` ができます。

```bash
$ fasta2json.py 2pv7.fast
```

### AlphaFold3の実行

floydでAlphaFold3を実行します。以下のslurmジョブスクリプト `af3.sh` をjsonファイルと同じフォルダに作成してジョブを投入します。GPUはメモリが空いているものを選ばないとエラーが出ると思うので、 `CUDA_VISIBLE_DEVICES` を指定してマニュアルで選びます。

```bash
#!/bin/bash
#SBATCH -p all
#SBATCH -J af3 # job name
#SBATCH -n 1  # num of total mpi processes
#SBATCH -c 8  # num of threads per mpi processes
#SBATCH --mail-type=ALL
#SBATCH -o %x_%j.log # %xにはjob名、%jにはjobIDが入る

export CUDA_VISIBLE_DEVICES="7" # 使用するGPUを指定

ALPHAFOLD3DIR='/opt/alphafold3'       # AlphaFold3のコードのディレクトリ
HMMER3_BINDIR="/opt/anaconda3/bin"    # HMMER3のバイナリディレクトリ
DB_DIR="/alphafold/public_databases"  # 配列・構造データベースのディレクトリ
MODEL_DIR="/opt/alphafold3/models"    # モデルパラメータのディレクトリ

source /opt/anaconda3/bin/activate AF3
/opt/anaconda3/envs/AF3/bin/python ${ALPHAFOLD3DIR}/run_alphafold.py \
    --jackhmmer_binary_path="${HMMER3_BINDIR}/jackhmmer" \
    --nhmmer_binary_path="${HMMER3_BINDIR}/nhmmer" \
    --hmmalign_binary_path="${HMMER3_BINDIR}/hmmalign" \
    --hmmsearch_binary_path="${HMMER3_BINDIR}/hmmsearch" \
    --hmmbuild_binary_path="${HMMER3_BINDIR}/hmmbuild" \
    --db_dir="${DB_DIR}" \
    --model_dir=${MODEL_DIR} \
    --json_path="2pv7.json" \
    --output_dir="."
```

ジョブを投入します。`--gres=gpu:a6000:1` はGPUをRTX A6000を1つ割り当てることを意味しますが、そもそもスクリプト内でGPUを手動で選んでいるのでここではあまり意味はありません（念のために付けているだけです）。

```bash
$ sbatch --gres=gpu:a6000:1 -w floyd af3.sh
```

たくさん配列をまとめて予測させたい場合は、ひとつのディレクトリにたくさんのjsonファイルをを作成して、 `--input_dir=<ディレクトリ名>` で指定すればよい。

また、時間がかかるMSAを再利用してligand等だけいろいろと試したい場合は[以下](https://qiita.com/Ag_smith/items/3bb110fe576292bbf0ea#化合物を変えた予測を高速に実行させる)を参照のこと

### 結果の可視化

[以下](https://qiita.com/Ag_smith/items/3bb110fe576292bbf0ea#予測結果の解釈)を参照のこと

