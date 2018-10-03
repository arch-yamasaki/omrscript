audiveris_on_docker
====
OMRソフトのAudiverisをdockerで動かす。



## Requirement
dockerのインストール。
`brew install docker`
でいけるはず...。

## Install and Usage

まず、gitからclone
```bash
git clone https://github.com/arch-yamasaki/omrscript
cd paths/omrscript/docker_audiveris
```

dockerイメージ作成。(最初はだいぶ時間かかる。)
```bash
docker build -t audiveris .
```
dockerコンテナ作成とログイン。
```bash
#dockerコンテナ起動。
docker run --name audiveris -v $PWD/images/:/home/audiveris/images/ -itd audiveris

# dokcerコンテナへの、ログイン。exit で出れる。
docker exec -it audiveris /bin/bash
```

コンテナ内でAudiverisコマンドを実行。
```bash
# コンテナ内での実行例。
# testにDichterliebe01.pdfに対するmusicXLをimages/testに出力する。
# imagesはホスト(動かしてるmac)とリンクしているので、外部から参照可能。
Audiveris -batch -export images/Dichterliebe01.pdf -output images/test
Audiveris -batch -export images/carmen.png -output images/test
Audiveris  -export images -output images/test

# これでpdfできると思うんやけど...エラー吐く。javaのエラーだから、コード自体がよくない気がする。Audiveris CLIはdev版らしいし。
Audiveris -batch -print Dichterliebe01.pdf -output images/test

# help
Audiveris -help

```

dockerの起動・停止。(ここはまあいらんちゃいらん。)
```bash

# コンテナを止めたいとき。
docker stop audiveris

# コンテナを起動したいとき。
docker start audiveris 

# コンテナの状態確認
docker ps # 起動してるコンテナだけ表示。
docker ps -a # 起動してないコンテナも表示。
```


musicSMLの楽譜化は[musicXML viewer](https://www.soundslice.com/musicxml-viewer/)がおすすめ。
appstoreにあるTEXviewというアプリでは一部上手くでないが、上記サイトは非常に綺麗に出る。
逆に言えばmusicXMLが完璧でもviewerシステム次第では綺麗に写らない。


## Licence

[MIT](https://github.com/tcnksm/tool/blob/master/LICENCE)

## Author

[tcnksm](https://github.com/tcnksm)