# 最新版スネークゲーム解説 - 日本語
![github contribution grid snake animation](https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake-dark.svg#gh-dark-mode-only)![github contribution grid snake animation](https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake.svg#gh-light-mode-only)


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
name: generate animation

on:
  # run automatically every 12 hours
  schedule:
    - cron: "0 */12 * * *" 
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the master branch
  push:
    branches:
    - main
    
  

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    
    steps:
      # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v2
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
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
![github contribution grid snake animation](https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake-dark.svg#gh-dark-mode-only)![github contribution grid snake animation](https://raw.githubusercontent.com/COfiftytwo/COfiftytwo/output/github-contribution-grid-snake.svg#gh-light-mode-only)
```
SNAKEが草を食べるように動いていたら完了。お疲れさまでした。
