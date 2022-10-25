# 判例フィッシュボーン
[裁判例検索](https://www.courts.go.jp/app/hanrei_jp/search1)で入手した判例のpdfからフィッシュボーン図を作成する研究です。  
## 環境
- python 3.10.5 (32bit)
- [MeCab 0.996](https://taku910.github.io/mecab/)
- [Text Mining Studio](https://www.msi.co.jp/tmstudio/)
## 構成
現在大きく分けて2つのプログラムがあります。
1. pdfからtextを抽出し、jsonファイルに変換
1. jsonファイルから時系列情報を抽出
## 概要
### 1. PDFテキスト抽出
PDFからテキストデータを抽出し、jsonファイルに変換します。
#### 手順
1. `t01_pdf2txt.py` でPDFから座標とテキストのデータをすべて取得
1. `t02_justify_sentence.py` でページごとにテキストを上から順番に並べる
1. `t03_detect_header.py` でテキストから見出しの候補を選出
1. `t04_split_section.py` で正しい見出しを洗い出し、見出し以外のテキストを本文として結合。最初の文を見出しのサブタイトル候補として分割
1. `t05_ignore_header_text.py` でサブタイトルを本文に結合（人手でサブタイトルかそうでないかを検出する予定だったが、応急処置）
1. `t06_split_centence.py` で、本文を「。」と『「」』「（）」で分割
### 2. 人物関係抽出
jsonファイルを読み込み、関係を抽出します。
まず、PDFからテキストデータを抽出したものと、それを係り受け解析したデータを用意します。
#### 手順
1. `t00_conbone_data.py` でテキストデータと係り受け解析データを一つのファイルに結合
1. `t01_extract_time.py` で時間表現を抽出
1. `t02_extract_people.py` で人物を抽出
1. `t03_extract_act.py` で行動を抽出
