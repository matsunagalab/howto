# 当日までの準備

## vimの使い方を勉強しておく

設定ファイルなどを作成、編集できるようになっておくため。具体的には、以下の教材の#01〜#08までを視聴しながら演習をこなしておく。

https://dotinstall.com/lessons/basic_vim

## GitHub education申請を済ませておく

GitHub copilotを使えるようにするため。以下を参考に学生申請をしておく(無料)。

https://qiita.com/SNQ-2001/items/796dc5e794ac3f57a945

## ChatGPT(OpenAI)のアカウント作成しておく


# Macの基本的な使い方

## Macの基本

https://help.apple.com/macos/big-sur/mac-basics/#appss

## Windowsとの違い

- ウィンドウを閉じてもアプリは終了していない
- Applicationフォルダへ入れることがインストール、その逆はアンインストール
- Windowsの `Ctrl` キーが Macの `Cmd` キーに相当する
- 右クリックがない。があるように設定することもできる(以下ではそのように設定する)

## 各種設定

- 左上のリンゴマークから「このMacについて」で自分のマシンの性能を確認
- マウス/トラックパッド/キーボードの設定
- Finderの設定 (Homeディレクトリをサイドバーに、全てのファイルを表示、リスト表示)
- Dockの設定(右側にする、アプリケーションフォルダの追加など)
- デスクトップを一つ増やす。デスクトップの移動。

## 覚えてほしいショートカットキー

- コピー `Cmd-c`
- ペースト `Cmd-v`
- 複製 `Cmd-d` (PowerPointやFinderでよく使う)
- Undo `Cmd-z`
- ウィンドウ/タブを閉じる `Cmd-w`
- アプリの終了 `Cmd-q`
- アプリ切り替え `Cmd-Tab`
- スクリーンショット `Cmd-Shift-5`
- Safariなど ページ送り `Space`
- Safariなど ページ戻し `Shift-Space`
- Safariなど URLへフォーカス `Cmd-l`
- Safariやターミナルなど 新しいタブの作成 `Cmd-t`
- Safariやターミナルなど タブの移動 `Cmd-Shift-矢印` `Cmd-Shift-[]`
- Finder ディレクトリの移動 `Cmd-上下矢印`

## 便利なアプリ

- 使用状況確認 Activity Monitor
- スポットライト または ランチャ Alfred (`brew install --cask alfred` でインストール)
- エディタ VSCode Emacs

## 良い慣習(Good practice)

- Homeディレクトリ直下にディレクトリを作成していく
- ファイル名またはディレクトリ名は「日付_内容」にする。そうすると時間順でファイル/ディレクトリが一覧できる
- ターミナルからも使用するファイル/ディレクトリの場合は、「内容」をできる限り英数字で書く(ターミナルから扱いやすいようにするため)
- 研究室ホームページをブックマークへ追加。ホームページのリンクを使う

---

# コマンドの初歩

以下でコマンドの解説を行っていきますが、自分で理解が不十分だなもっと練習したいなと思った場合は事後学習として以下の教材を受講してください。

https://prog-8.com/lessons/commandline/study/1

## ターミナルの設定

- ターミナルの起動
- Dockへの追加
- ターミナルの設定(フォントサイズ、背景の透過など)
- タブの使用

## シェルの機能

- シェルとは？
- Tab補完
- ワイルドカード `*` `?`
- 履歴の呼び起こし
- 履歴のインクリメンタル検索 `Ctrl-r` (履歴に関しては http://0xcc.net/unimag/3/ )
- 一度手入力した長めのコマンドは二度と手入力しないように、履歴を使いこなすことを心がける

## ショートカットキー

- Emacs keybindings [Emacsのキーバインド覚書](https://www.aise.ics.saitama-u.ac.jp/~gotoh/EmacsKeybind.html)
- 一文字先 `Ctrl-f`
- 一文字前 `Ctrl-f`
- カーソル上の文字を削除 `Ctrl-d`
- カーソル上の一つ前を削除 `Ctrl-h`
- 行先頭 `Ctrl-a`
- 行末尾 `Ctrl-e`
- 一つ前のコマンド `Ctrl-p`
- 一つ後のコマンド `Ctrl-n`
- 履歴のインクリメンタル検索 `Ctrl-r`

## パスの概念

- 絶対パス
- 相対パス
- ドット(.)の意味。チルダ(~)の意味

## 基本的コマンド

- 現在のディレクトリの表示(print working directory) `pwd`
- ディレクトリの移動(chand directory) `cd` `cd -`
- ファイル/ディレクトリの一覧(list) `ls` `ls -l` `ls -al` `ls -rtl`
- ファイル/ディレクトリのコピー `cp` `cp -r`
- ファイル/ディレクトリの移動 `mv`
- ファイルの削除 `rm` `rm -f`
- ディレクトリの作成 `mkdir`
- ディレクトリの削除 `rm` `rm -r` `rm -rf`
- 履歴表示 `history`
- テキストファイルの中身を表示(concatenate) `cat`
- 文字数や行数を数える `wc` `wc -l`
- ファイル内の文字列検索 `grep`
- ファイルの検索 `find` `mdfind`
- 画面の文字を表示 `echo`
- 管理者権限で実行 `sudo`
- 使用状況確認 `htop` (`brew install htop` でインストール)
- Finderで開く `open`
- コマンドのマニュアルを読む `man`
- 番外編 音声読み上げ `say`、コピー `pbcopy`

## ページャless

- ページ送り(`SPC`)、ページ戻し(`b`)
- 検索(`/クエリ文字列`)、次の候補へ移動(`n`)、前の候補へ移動(`Shift+n`)
- 終了(`q`)、vimを起動(`v`)
- PDBデータを`less`で見てみる

## 環境変数

- `HOME` ( `echo $HOME` で確認) 
- `PATH` ( `echo $PATH` で確認)
- `PATH`に current directory が含まれていない理由
- `which` コマンドの紹介

## dotファイル

- dotファイルは設定ファイル。環境変数などを定義。`ls -a` で表示できる
- `~/.zshrc` シェルの設定ファイル
- `~/.zsh_history` コマンドの履歴が保存されるファイル

## ターミナル上でテキストファイルを編集

- ターミナル上でぱぱっと使うエディタとしては vim がお手軽で便利。dotファイルなどはvimで編集。

# 課題

1. vimを使って、`~/.zshrc` へ以下の設定を追加してください。lsをカラー化したり保存される履歴などを増やします。

```bash
# prompt
autoload colors
colors
PROMPT="%{$fg[magenta]%}%n@%m%(!.#.$)%{$reset_color%}:%c$ " # 左側に表示
PROMPT2="%{$fg[green]%}%_> %{$reset_color%}" # 2行以上のコマンド
SPROMPT="%{$fg[red]%}correct: %R -> %r [nyae]? %{$reset_color%}" # コマンド候補提示
# RPROMPT="%{$fg[cyan]%}[%~]%{${reset_color}%}" # 右側に表示
RPROMPT=""

# zsh-completions(補完機能)の設定
if [ -e /usr/local/share/zsh-completions ]; then
    fpath=(/usr/local/share/zsh-completions $fpath)
fi
autoload -U compinit
compinit -u

# ls に色を付ける
export LSCOLORS=exfxcxdxbxegedabagacad
export LS_COLORS='di=34:ln=35:so=32:pi=33:ex=31:bd=46;34:cd=43;34:su=41;30:sg=46;30:tw=42;30:ow=43;30'
alias ls="ls -GF"
alias gls="gls --color"
zstyle ':completion:*' list-colors 'di=34' 'ln=35' 'so=32' 'ex=31' 'bd=46;34' 'cd=43;34'

# コマンド履歴
HISTSIZE=1000000
SAVEHIST=1000000
setopt share_history

# コマンド履歴検索
autoload history-search-end
zle -N history-beginning-search-backward-end history-search-end
zle -N history-beginning-search-forward-end history-search-end
bindkey "^P" history-beginning-search-backward-end
bindkey "^N" history-beginning-search-forward-end

# ディレクトリ名を入力するだけで移動
setopt auto_cd

# 移動したディレクトリを記録しておく。"cd -[Tab]"で移動履歴を一覧
setopt auto_pushd

# コマンド訂正
setopt correct

# 補完候補を詰めて表示する
setopt list_packed

# 補完候補表示時などにピッピとビープ音をならないように設定
setopt nolistbeep

# Emacsライクキーバインド設定
bindkey -e 

# ターミナルの文字コードの設定
export LC_CTYPE=ja_JP.UTF-8

# デフォルトのエディタ
export EDITOR=vim
```

2. `find` と `mdfind` の実用的なオプションを調べて、試してみてください。

3. シェルの機能であるパイプとリダイレクションについてネットで調べてください。パイプを使って面白いワンライナーを作ってみてください。

# Anacondaのインストール

https://www.anaconda.com/download/success

- インストール手順の説明
- インストール場所の確認
- 仮想環境の説明
- condaコマンドの簡単な説明

# VSCodeのインストールとJupyter

```bash
$ brew install --cask visual-studio-code
```

- 画面レイアウトの説明
- フォルダやファイルの開き方
- キーボードショートカットの説明 (Cmd-Shift-p, Cmd-f, Cmd-Shift-f, Cmd-b, Opt-Shift-Down)
- Extensionsのインストール (Python, Jupyter, Copilot)
- VSCodeからのJupyterの使い方
- Copilotの使い方
