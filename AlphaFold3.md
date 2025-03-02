# AlphaFold3の実行方法

以下の作業をfloyd上で行います。

### Input fileの準備

以下のようなJSONを用意します。 `2pv7.json` とします。

```
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

または、fastaからjsonへコンバートするツールを使うことも出来ます。ここでは、floydにインストールした `fasta2json.py` を使います。

FASTAを用意します。 `2pv7.fasta` とします。 `#2`はhomo-dimerを意味します。詳しくはツール元の https://github.com/snufoodbiochem/Alphafold3_tools?tab=readme-ov-file をご覧ください。

```
>2PV7 #2
GMRESYANENQFGFKTINSDIHKIVIVGGYGKLGGLFARYLRASGYPISILDREDWAVAESILANADVVIVSVPINLTLETIERLKPYLTENMLLADLTSVKREPLAKMLEVHTGAVLGLHPMFGADIASMAKQVVVRCDGRFPERYEWLLEQIQIWGAKIYQTNATEHDHNMTYIQALRHFSTFANGLHLSKQPINLANLLALSSPIYRLELAMIGRLFAQDAELYADIIMDKSENLAVIETLKQTYDEALTFFENNDRQGFIDAFHKVRDWFGDYSEQFLKESRQLLQQANDLKQG
```

以下でjsonファイルへコンバートします。PATHは通っています。これで `2pv7.json` ができます。

```
$ fasta2json.py input.fast
```

### AlphaFold3の実行

floydでAlphaFold3を実行します。以下のslurmジョブスクリプト `run.sh` を作成してジョブを投入します。GPUはメモリが空いているものを選ばないとエラーが出ると思うので、 `CUDA_VISIBLE_DEVICES` を指定してマニュアルで選びます。

```
#!/bin/bash
#SBATCH -p all
#SBATCH -J af3 # job name
#SBATCH -n 1  # num of total mpi processes
#SBATCH -c 32  # num of threads per mpi processes
#SBATCH --mail-type=ALL
#SBATCH -o %x_%j.log # %xにはjob名、%jにはjobIDが入る

export CUDA_VISIBLE_DEVICES="7" # 使用するGPUを指定

ALPHAFOLD3DIR='/opt/alphafold3'       # AlphaFold3のコードのディレクトリ
HMMER3_BINDIR="/opt/anaconda3/bin"    # HMMER3のバイナリディレクトリ
DB_DIR="/alphafold/public_databases"  # 配列・構造データベースのディレクトリ
MODEL_DIR="/opt/alphafold3/models"    # モデルパラメータのディレクトリ

conda activate AF3
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
