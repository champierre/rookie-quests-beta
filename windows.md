# Windows の自分の PC で進めるとき

クエストの README と授業は **GitHub Codespaces** で進める前提で書いてあります。Codespaces を使えず、Windows の自分の PC で進めるときだけ、このページを読んでください。

Codespaces のターミナルは Linux です。Windows のターミナル（PowerShell）では、ファイルを操作するコマンドの一部が違います。このページは、その違いをまとめたものです。`python` と `git` のコマンド（`python quest.py --stage 1`、`git add` など）は、どちらでも同じです。

## 最初に用意するもの

| 用意するもの | 内容 |
|---|---|
| Python 3.10 以降 | [python.org](https://www.python.org/downloads/) から入れます。インストールの最初の画面で **Add python.exe to PATH** にチェックを入れます |
| Git | [Git for Windows](https://git-scm.com/download/win) を入れます |
| VS Code | ファイルを開いて書くのに使います（[code.visualstudio.com](https://code.visualstudio.com/)） |
| ターミナル | **PowerShell** を使います。VS Code の中のターミナル（**表示** → **ターミナル**）でもかまいません |

入れたら、PowerShell で次を実行して確かめます。

    python --version
    git --version

`python` で Microsoft Store が開いたり、何も起きなかったりするときは、`python` の代わりに `py` を使ってください（例：`py quest.py --stage 1`）。

## fork を自分の PC に持ってくる（clone）

Codespaces では、fork の中身が最初から開いています。自分の PC では、fork を一度だけ **clone** します。

    cd ~
    git clone https://github.com/YOUR-ID/rookie-quests-beta.git
    cd rookie-quests-beta

`YOUR-ID` は自分の GitHub ID です。次からは、PowerShell を開いたら `cd ~\rookie-quests-beta` でこのフォルダに移動します。

新しいクエストを受け取るときは、Codespaces と同じです（fork で **Sync fork** を押してから `git pull`）。

## コミットに出る名前とメールを設定する

Codespaces では、コミットに記録される名前とメールが自動で設定されます。自分の PC では、自分で設定します。**本名と本物のメールアドレスは使いません**（コミットは公開されます）。

    git config --global user.name "YOUR-ID"
    git config --global user.email "NOREPLY-ADDRESS"

`NOREPLY-ADDRESS` には、GitHub の **Settings** → **Emails** で **Keep my email addresses private** にチェックを入れたときに表示される、`…@users.noreply.github.com` で終わるアドレスを、そのまま写します。

## コマンドの読み替え

README に出てくるコマンドのうち、PowerShell では書き方が違うものです。

| README のコマンド（Codespaces） | PowerShell | 出てくるところ |
|---|---|---|
| `export NAME=value` | `$env:NAME = "value"` | Quest 7（環境変数の設定）。PowerShell を閉じるまで有効なのは同じです |
| `grep -rn "words from the error" forum/` | `git grep -n "words from the error" -- forum/` | Quest 9（フォーラムを検索する）。VS Code の `Ctrl+Shift+F` でも検索できます |
| `mkdir -p team` | `mkdir team -Force` | Quest 14 ステージ3 |
| `cp quest-14/team-page.md team/YOUR-ID.md` | `Copy-Item quest-14\team-page.md team\YOUR-ID.md` | Quest 14 ステージ3 |
| `cp -r welcome/_template welcome/YOUR-ID` | `Copy-Item -Recurse welcome\_template welcome\YOUR-ID` | 第14回（新人のためのクエスト） |
| 空のファイルを作る（`visitor.badge` など） | `New-Item visitor.badge -ItemType File` | Quest 0 ステージ2 |
| `ls` | `ls`（そのまま使えます） | |
| `cd ..`、`cd ~` | そのまま使えます | |

`cd`、`ls`、`git`、`python` のコマンドでは、パスの区切りは `/` のままでも動きます。

## 気をつけること

**ファイル名の最後に `.txt` が付いてしまう**

メモ帳でファイルを作ると、`visitor.badge` のつもりが `visitor.badge.txt` になることがあります。エクスプローラーでは拡張子が隠れているので、気づきにくいです。空のファイルは、上の表の `New-Item` で作るか、VS Code の **ファイル** → **新しいファイル** で作ってください。名前は `ls` で確かめられます。

**`git commit` でエディタが開いた**

`-m "..."` を付けずに `git commit` を実行すると、エディタが開きます。どのエディタが開くかは、Git を入れたときの選び方で決まります。Vim が開いたら、`Esc` を押してから `:wq` と入力して `Enter` で閉じます。メモ帳や VS Code が開いたら、メッセージを書いて保存し、閉じます。

**`help()` の表示から戻れない**

`python -c "import phonebook; help(phonebook)"` などで表示が止まったら、`q` を押して戻ります。

**Quest 14・18 のステージ3のチェックが「API の上限」で止まる**

チェックのプログラムは GitHub の API を読みます。Codespaces では GitHub の鍵（`GITHUB_TOKEN`）を使いますが、自分の PC にはありません。鍵がなくても動きますが、1時間に読める回数が少なくなります。上限で止まったら、1時間ほど待ってから、もう一度実行してください。

**改行の変換**

Git for Windows は、ふつう、ファイルを取り出すときに改行を Windows の形（CRLF）に変え、コミットするときに元の形（LF）に戻します。クエストを進めるうえで、気にする必要はありません。`git status` で、変えていないファイルが変更ありと表示されるときは、先生に相談してください。

## 困ったとき

自分の PC で解けないときは、Codespaces で同じクエストを開いてください。Codespaces は、自分の fork の **Code** → **Codespaces** から、いつでも使えます（毎月の無料の時間の中で）。
