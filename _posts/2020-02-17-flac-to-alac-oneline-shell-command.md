---
layout:     post
date:       2020-02-17 20:13:06 +0900
category:   blog

title: |
  macOSでflacをalacに変換するワンライナー
---

最近moraでミリマス楽曲のロスレスとか買うようになったので

<!--more-->

必要なものはFFmpegなので`brew install ffmpeg`とかで入れておく

moraDownloaderでダウンロードしたflacをalacに変換するワンライナー。別の方法でダウンロードしたものは`~/Music/mora/**/*.flac`を`~/Downloades/**/*.flac`とかに適宜置き換えてください
```zsh
for i in ~/Music/mora/**/*.flac; do if test ! -e "${i:r}.m4a"; then ffmpeg -i "$i" -c:a alac -c:v copy "${i:r}.m4a"; fi; done
```

ついでにシェルスクリプト。`$ ./flac-to-alac ~/Downloads`とかやって好きにディレクトリ変えられる
```zsh
#!/bin/zsh

dir=${1:-~/Music/mora}

for i in ${dir}/**/*.flac; do
  if test ! -e "${i:r}.m4a"; then
    ffmpeg -i "$i" -c:a alac -c:v copy "${i:r}.m4a"
  fi
done
```

