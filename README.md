# 最新版スネークゲーム解説 - 日本語（2023年10月8日修正）
<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake-dark.svg"
  />
  <source
    media="(prefers-color-scheme: light)"
    srcset="https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake.svg"
  />
  <img
    alt="github contribution grid snake animation"
    src="https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake.svg"
  />
</picture>


手順１：リポジトリを作成する<br>
Repository nameは好き名前を。作成の際「Add a README file」にチェックを忘れないこと。
<br>

手順２：yamlファイルを作る。<br>
今回はyamlファイルについての説明はしません。リポジトリを作成すると、右上に「Add file」から「Create new file」をクリック。<br>
「Name your file...」に「.github/workflows/～～.yaml」をコピペし～～を好きなファイル名に変更して、「Commit chenges」をクリック。
<br>

手順３：yamlファイルに下のコードをコピペする。<br>
コピぺするときに注意することは、メインのブランチが「main」か「master」かを確認すること。そして「branches:」のところに入力し「Commit chenges」をクリック。
<br>

```
name: Generate-Fancy-Snake-Header

on: 
  push:
    branches:
      - main
  schedule: # execute every 24 hours
    - cron: "0 */24 * * *"
  workflow_dispatch:

jobs:
  generate:
    name: Animate snake
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - name: Generate snake animation
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          
      - name: Push snake animation to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
手順４：READMEファイルに戻って下のコードをコピペする。
READMEファイルに戻って下のコードをコピペして、「COfiftytwo/COfiftytwo」のところを「自分のユーザー名/今回作ったリポジトリ名」に変更して、「Commit chenges」をクリック。
```
<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake-dark.svg"
  />
  <source
    media="(prefers-color-scheme: light)"
    srcset="https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake.svg"
  />
  <img
    alt="github contribution grid snake animation"
    src="https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake.svg"
  />
</picture>
```
SNAKEが草を食べるように動いていたら完了。お疲れさまでした。
