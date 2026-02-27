

# SeaSideX ビルドガイド
- [SeaSideX ビルドガイド](#seasidex-ビルドガイド)
  - [1. 注意事項](#1-注意事項)
    - [1-1. 対応するキーボード](#1-1-対応するキーボード)
    - [1-2. ケースとの干渉](#1-2-ケースとの干渉)
    - [1-3. ZMKファームウェアの使用](#1-3-zmkファームウェアの使用)
    - [1-4. KeyballでできてSeaSideでできないこと](#1-4-keyballでできてseasideでできないこと)
    - [1-5. 組み立ての大変さとLiPoバッテリーの取り扱い](#1-5-組み立ての大変さとlipoバッテリーの取り扱い)
    - [1-6. LED配線によるバッテリー持続時間の違い](#1-6-led配線によるバッテリー持続時間の違い)
  - [2. 準備](#2-準備)
    - [2-1. キット同梱品確認](#2-1-キット同梱品確認)
    - [2-2. 組立前にお客様自身で準備いただく部品](#2-2-組立前にお客様自身で準備いただく部品)
      - [2-2-1. バッテリーの選び方と注意点](#2-2-1-バッテリーの選び方と注意点)
    - [2-3. 必要な工具](#2-3-必要な工具)
  - [3. 組み立て](#3-組み立て)
    - [3-1. ポゴピンの取り付け（一部）](#3-1-ポゴピンの取り付け一部)
    - [3-2. スイッチの取り付け](#3-2-スイッチの取り付け)
    - [3-3. マイコンの足をカット](#3-3-マイコンの足をカット)
    - [3-4. バッテリーコネクタの取り付け](#3-4-バッテリーコネクタの取り付け)
    - [3-5. コンスルーの取り付け](#3-5-コンスルーの取り付け)
    - [3-6. ポゴピン残りのはんだ付け（ボール側のみ）](#3-6-ポゴピン残りのはんだ付けボール側のみ)
    - [3-7. マイコンのはんだ付け](#3-7-マイコンのはんだ付け)
    - [3-8. 使用モデルに応じた配線](#3-8-使用モデルに応じた配線)
      - [3-8-1. SeaSide39用配線](#3-8-1-seaside39用配線)
      - [3-8-2. SeaSide44用配線](#3-8-2-seaside44用配線)
      - [3-8-3. SeaSide39(左手トラボ)用配線](#3-8-3-seaside39左手トラボ用配線)
    - [3-9. トラックボールセンサーのはんだ付け](#3-9-トラックボールセンサーのはんだ付け)
    - [3-10. LED配線カット](#3-10-led配線カット)
    - [3-11. 組み立て](#3-11-組み立て)
  - [4. ファームウェア](#4-ファームウェア)
    - [4-1. テスト用ファームウェアのダウンロード](#4-1-テスト用ファームウェアのダウンロード)
    - [4-2. テスト用ファームウェアの書き込みとペアリング](#4-2-テスト用ファームウェアの書き込みとペアリング)
    - [4-3. 動作確認](#4-3-動作確認)
    - [4-4. ZMK Studioの活用](#4-4-zmk-studioの活用)
    - [4-5. ZMKファームウェアのカスタマイズとビルド方法](#4-5-zmkファームウェアのカスタマイズとビルド方法)
  - [5. お疲れさまでした](#5-お疲れさまでした)

![DSC02063](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC02063.JPG)

<a id="1-注意事項"></a>
## 1. 注意事項

**※ 購入前にお読みください**

SeaSideXで無線化を行うにあたり、いくつかの制約や注意事項があります。\
これらの内容をご理解いただいた上でのみ、ご購入をお願いいたします。

<a id="1-1-対応するキーボード"></a>
### 1-1. 対応するキーボード

~~本キットは私の個人的な「愛用のKeyball39を無線化して使いたい！」という気持ちが出発点にあるため、右手トラックボール版のKeyball39専用に設計されています。~~\
~~そのため、現時点では左手トラックボールのKeyball39や、トラックボールの配置を問わずKeyball44およびKeyball61では使用できません。~~\
~~右手トラックボール版のKeyball39以外でSeaSide39を使用した場合のあらゆるトラブルに対しては対応が困難であることをご了承ください。~~

~~なお、左手トラックボール版やKeyball44、Keyball61も無線化してほしいという要望を数件いただいております。今後開発を進めていきたいと考えてはいますが手元にそれらのキーボードが無く着手が難しい状況ですので、開発用にこれらのキーボードをお貸しいただける方がいらっしゃいましたら、ぜひご連絡いただけると幸いです。~~

2025年6月販売分より対応機種を大幅に追加いたします！\
対応状況は以下の通りです。

| | 右手トラックボール | 左手トラックボール |
|:---|:---:|:---:|
| Keyball39 | ◯ | ◯ |
| Keyball44 | ◯ | △ |
| Keyball61 | ✕ | ✕ |
| Keyball39ish | ◯ | ◯ |
| Keyball44ish | ◯ | △ |
| Keyball61ish | ✕ | ✕ |

△ : 技術的には対応可能ですが動作確認できる実機がないためた未着手の状態です。要望が多ければ対応予定ありです。\
✕ : 技術的にSeaSideXでの無線化は厳しい状態です。今後も対応予定は無いと思ってください。

また、使用するモデルによって一部組み立て工程に違いがあります。ビルドガイドをよく読み、間違えないようご注意ください。

※ Keyballishとは、Keyballをロープロファイル化・狭ピッチ化したKeyballの互換キーボードです。詳細：[Keyballishシリーズに関して](https://note.com/kazu_dob/n/n25c60390b9b3) \
開発者のKzさんにもご協力いただきSeaSideXでKeyballishに対応することができました！\
ish対応版のSeaSideXを使用する際にはNoballSideの基板がish専用のものとなるため、通常版Keyballとの互換性はありませんのでご了承ください。

<a id="1-2-ケースとの干渉"></a>
### 1-2. ケースとの干渉

SeaSideXは可能な限りKeyballの資源を再利用したいという思想で設計していますが、どうしても構造上USB端子の位置をPro Microと同じにすることができませんでした。\
ですので、多くのKeyball用ケースとSeaSideXのUSB端子が干渉してしまうという欠点があります。\
↓過去に作成したKeyball39用ケースの場合
![DSC00409](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00409.JPG)

対応方法としては以下のいずれかになると思います。参考にしていただき、許容できると感じる方のみご購入をお願いいたします。

- 充電やファームウェアの書き込みを行う際のみケースを外す
  - 手間ではありますが、バッテリー持ちは決して悪くないので現実的な選択肢だと思います。カバーに格納できる200mAhのバッテリーでも1~2週間ほどは充電無しで連続利用が可能です。
- 干渉する箇所を切る・削るなどの加工を行う
  - 加工する際は自己責任でお願いいたします。
- 専用ケースを使う
  - お手持ちのケースを使い続けることにこだわりが少ない方は、SeaSideX専用に設計したケースをお使いいただくことも可能です。底面に最大1000mAhまでの大容量バッテリーを搭載できるケースもありますのでぜひご検討ください。1000mAhのバッテリーを使用した場合、1ヶ月以上は充電無しで連続利用が可能です。

<a id="1-3-zmkファームウェアの使用"></a>
### 1-3. ZMKファームウェアの使用
SeaSideXでは、マイコンがPro MicroからXIAO BLEに変更されるため、ファームウェアもQMKからZMKに変更となります。これにより、以下のような使い勝手の変化があることをご了承ください：

- Remap等のGUI上でのキーマップ変更ツールが使用できなくなります
  - SeaSideXはZMK Studioというツールにも対応しており、これを使用すればRemapに近い操作感でキーマップの変更も可能ではありますが、機能に制限があり、より複雑な設定を行う場合は結局ファームウェアを直接編集する必要が出てくることが多いです
- キーマップの変更や複雑な設定の変更にはGitHubを使用したファームウェアのビルドが必要になります
- Bluetoothの接続先の切り替えなど、無線特有の操作方法を覚える必要があります

ZMKファームウェアは比較的新しいファームウェアであるため、QMKと比較すると機能面で一部制限があります。しかし、無線化のメリットを享受するためには必要な変更となりますので、これらの違いを許容いただける方のみご購入をお願いいたします。

なお、ZMKファームウェアのビルドや書き込み方法については後述のビルドガイド内「[4. ファームウェア](#4-ファームウェア)」セクションで詳しく説明します。

<a id="1-4-keyballでできてseasideでできないこと"></a>
### 1-4. KeyballでできてSeaSideでできないこと

キーマップを含むQMKファームウェアでの設定内容はZMKに流用できないため、すべてご自身で同等の設定をし直していただく必要があります。あまりないとは思いますが、ファームウェアの違いにより実現自体できなくなる機能が存在する可能性もありますのでご了承ください。

また、ハードウェア面ではSeaSideXでは以下の機能が使用できなくなります。
- RGBLEDは点灯しなくなります
- OLEDディスプレイが使用できなくなります（SeaSideX装着時にOLEDを接続しないでください）
- TRRSケーブルが使用できなくなります（SeaSideX装着時にTRRSケーブルを接続しないでください）
- Keyballのリセットボタンは機能しなくなります

これらの制限は無線化に伴う仕様変更によるものですので、あらかじめご理解いただけますようお願いいたします。

<a id="1-5-組み立ての大変さとlipoバッテリーの取り扱い"></a>
### 1-5. 組み立ての大変さとLiPoバッテリーの取り扱い

無線化という性質上、このキットではLiPoバッテリーを扱います。また、細かいはんだ付け作業も必要となります。\
LiPoバッテリーの取り扱いには多少なりともリスクが伴います。他にもはんだ付け作業のミスによる基板や部品の損傷など、様々なトラブルが発生する可能性があります。\
当キットは個人開発のため、自己責任での組み立てとなること、およびすべてのトラブルに対応しきれない場合があることをご理解ください。

<a id="1-6-LED配線によるバッテリー持続時間の違い"></a>
### 1-6. LED配線によるバッテリー持続時間の違い

KeyballではオプションでRGBLEDの実装が可能ですが、先述のとおりSeaSideXではLEDは点灯しなくなります。\
しかし点灯しないLEDが少量の待機電力を消費しており、その待機電力によりバッテリーの持続時間がLED配線をしていないものに比べ短くなる可能性があります。\
私の手元で検証したバッテリー持続時間（200mAhで1週間超、1000mAhで1ヶ月超持続）はLEDが配線されていないKeyballで使用した場合の実績値ですが、LED配線済のKeyballで200mAhが3日程度で切れたという報告もありました。\
私の手元にLED配線済のKeyballがなく検証が不十分で申し訳ありませんが、この点ご理解いただきますようお願いいたします。\
追記：こちらは以下手順 [3-10. LED配線カット](#3-10-LED配線カット)を行うことで対処可能です。

<a id="2-準備"></a>
## 2. 準備

制作を始める前に、まずは必要なものがすべて揃っていることをご確認ください。

<a id="2-1-キット同梱品確認"></a>
### 2-1. キット同梱品確認

| 名前 | 数 | 備考 |
|:-|:-|:-|
| メイン基板BallSide | 1枚 | |
| メイン基板NoBallSide | 1枚 | ish版を購入した場合ish専用基板に変更 |
| トラックボール用基板 | 1枚 | 省電力化のため置き換え |
| ポゴピン(2ピン) | 3本 | |
| コンスルー(12ピン) | 4本 | |
| トラックボール用センサー(PMW3610DM-SUDU) | 1個 | [データシート](https://www.alldatasheet.jp/datasheet-pdf/pdf/899003/PIXART/PMW3610DM-SUDU.html) |
| トラックボールセンサー用レンズ | 1個 | センサーに同梱されています |
| バッテリー用コネクタ | 2本 | JST 1.25mm 2pin|
| スライドスイッチ | 2個 | |
| マイコンカバー | 2個 | カバーセットを購入した方のみ |
| 専用ケース | 2個 | ケースセットを購入した方のみ |
| 大容量ケース | 2個 | 大容量ケースセットを購入した方のみ |
| 大容量ケース底部パーツ | 2個 | 大容量ケースセットを購入した方のみ |
| M2ネジ 8mm | 6本 | 大容量ケースセットを購入した方のみ |


![IMG_1063](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1063.jpg)

<a id="2-2-組立前にお客様自身で準備いただく部品"></a>
### 2-2. 組立前にお客様自身で準備いただく部品

| 名前 | 数 | 備考 |
|:-|:-|:-|
| マイコン Seeed XIAO BLE nRF52840 | 2個 |  |
| Lipoバッテリー | 2個 | 推奨バッテリーについては後述します |
| バッテリーコネクタ | 2本 | 用意したバッテリーのコネクタがJST 1.25mmでない方のみ |

SeaSideXはamazonで購入できる以下のバッテリーのサイズを基準に設計していますので、以下のバッテリーの購入をおすすめします。どちらも2個入りで、JST 1.25mmコネクタ仕様になっているので付属のコネクタに接続可能です。\
これ以外のバッテリーを使用する場合、JST 1.25mmコネクタ以外のものを仕様するには別途コネクタを用意する必要があるためご注意ください。

200mAh : https://www.amazon.co.jp/dp/B08XJZZMN3 \
マイコンカバーにピッタリ格納できるサイズです。この大きさでも1〜2週間は充電無しで連続利用可能です。（LED配線無しの場合）

1000mAh : https://www.amazon.co.jp/dp/B098DRP9WX \
大容量ケースにピッタリ格納できるサイズです。この大きさ以下であれば大抵のバッテリーが入るはずですので幅広くお選びいただけます。1000mAhあると、1ヶ月以上は充電無しで連続利用可能です。（LED配線無しの場合）

追記：上記のおすすめバッテリーが2025/07/10現在欠品中のようです。代わりのバッテリーを探す際に重要な観点を記載しましたので参考にしてみてください。[2-2-1. バッテリーの選び方と注意点](#2-2-1-バッテリーの選び方と注意点)

LED配線済のバッテリー持続時間の注意点については「[1-6. LED配線によるバッテリー持続時間の違い](#1-6-led配線によるバッテリー持続時間の違い)」セクションをご確認ください。


<a id="2-2-1-バッテリーの選び方と注意点"></a>
#### 2-2-1. バッテリーの選び方と注意点

バッテリーをご自身で探す場合の選び方と注意点を説明します。

- 観点１. 大きさ\
  lipoバッテリーのサイズは「502025」のように記載され、2桁ずつ厚み・縦・横のサイズを示しています。この例の場合だと厚さ5mm, 縦20mm, 横25mmとなります。\
  これを踏まえ、SeaSideXで推奨しているバッテリーのサイズは以下となります。
  | バッテリー格納場所 | 推奨バッテリーサイズ | サイズ詳細 |
  |:---|:---|:---|
  | マイコンカバー内 | 502025 | 厚さ5mm, 縦20mm, 横25mm |
  | 大容量ケース底面 | 803040 | 厚さ8mm, 縦30mm, 横40mm |

  こちらのサイズを超えないようにお選びいただけますと基本的に使用可能となります。\
  マイコンカバーに収める場合は厚みに少し余裕がありますので752025などでも収まるかもしれません。（実機では未確認となりますのでご了承ください）
  ![IMG_lipo](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_lipo.jpg)

- 観点2. コネクタ\
  付属のコネクタに適合する規格は先述のとおり、JST 1.25mmと記載のものになります。\
  また、コネクタの規格自体が同じでもバッテリーの極性が逆になっているバッテリーも数多く存在します。極性が逆になっているものをそのまま接続するとマイコンが故障してしまうためご注意ください。\
  極性が逆になっているバッテリーを購入した場合でも、SeaSideX基板側バッテリーコネクタの極性を逆にはんだ付けすることで使用が可能です。\
  バッテリーの商品ページとSeaSideXに接続するタイミングで正しい配線になっているか十分に確認の上でご利用をお願いいたします。
  
  正しい極性のコネクタ
  ![IMG_1516](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1516.jpg)

  極性が逆のコネクタ例
  ![IMG_lipo2](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_lipo2.jpg)

<a id="2-3-必要な工具"></a>
### 2-3. 必要な工具

SeaSideXの組み立てには下記の工具が必要です。

| 名前 | 備考 |
|:-|:-|
| はんだごて | 温度調整可能なもの推奨 |
| はんだ | |
| ニッパー|ピンヘッダの切断およびバッテリーコネクタ配線の被覆剥き用 |
| ドライバー ||
| ピンセット ||
| 両面テープ|バッテリー固定用|

<a id="3-組み立て"></a>
## 3. 組み立て

ここからはんだ付け作業に入ります。\
特に断りがない作業はどのKeyballでも・左右どちらの基板でも同じ作業をすると読み取ってください。基板を「右側・左側」と呼ぶ場合がありますが左トラボで使用予定の人は「ボール側・ボール無し側」と読み替えてください。\
また、Keyballish版を組み立てる場合、ボール無し側基板はSeaSideXishと書かれているものとなります。組み立て工程は通常版と同じです。\
一部画像がSeaSideXになる前のSeaSide39基板のままとなっている箇所がありますが、組み立てに影響は無いはずですのでご了承ください。

<a id="3-1-ポゴピンの取り付け（一部）"></a>
### 3-1. ポゴピンの取り付け（一部）

マイコン背面のパッドで信号を受け取るためのポゴピンを取り付けます。\
組み立ての都合で、現時点ではまだはんだ付けしないピンがあるので注意してください。

1. 写真を参考に、ポゴピンを装着する場所を確認します。右側は２箇所、左側は１箇所です。
![IMG_1062](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1062.jpg)


1. 対象のスルーホールにポゴピンを差し込みます。差し込む基板の面とポゴピンの向きを間違えないように注意してください。ロゴがある面に、段差があり根本まで差し込めないほうのピンを差し込むのが正解です。\
  ポゴピンの差し込み向き間違いによりお問い合わせを数多くいただいております。逆向きにはんだ付けしてしまうと最悪基板ごと交換になる場合もありますので慎重にご確認のうえお取り付けください。
  ![DSC00027](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00027.JPG)

1. 基板を裏返し、ポゴピンが固定されるようにマスキングテープなどで固定してください。裏面にポゴピンの足が少し飛び出していればOKです。
![DSC00028](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00028.JPG)

1. この状態でポゴピンの足をはんだ付けします。この時、右側基板のポゴピンの足を１本だけはんだ付けしないでおいてください。はんだ付けせずに残す箇所は画像で確認してください。左側基板はすべてはんだ付けしてOKです。
![DSC00032](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00032.JPG)


<a id="3-2-スイッチの取り付け"></a>
### 3-2. スイッチの取り付け

電源スイッチを基板に取り付けます。

1. スライドスイッチを基板の表面から差し込み、マスキングテープなどで固定します。
![DSC00034](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00034.JPG)

2. 裏面からはんだ付けします。スイッチが浮かないように注意してください。
3. 気になる方ははみ出した足をカットしてください。
![DSC00035](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00035.JPG)


<a id="3-3-マイコンの足をカット"></a>
### 3-3. マイコンの足をカット

後の工程に備え、マイコン（Seeed XIAO BLE nRF52840）のピンを長さをカットします。\
※ この工程は行わなくても組み立て可能です。組み立て済みをご注文いただいた方は、この工程が行われていないものが届く場合がありますのでご了承ください。

1. マイコンに付属のピンヘッダをマイコンにはんだ付けします。SeaSide専用カバーを使用する場合、マイコン上面にピンが長くはみ出しているとカバーと干渉する場合があるので注意してください。画像のようになっていればOKです。
![DSC00036](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00036.JPG)
   
2. マイコンの足を基板のスルーホールに差し込みます。差し込む箇所は画像で確認してください。
![DSC00413](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00413.JPG)

1. ポゴピンが押し込まれ、これ以上差し込めないことを確認したら、その状態でピンのはみ出している部分をニッパーでカットします。画像のようになればOKです。
![DSC00046](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00046.JPG)
  
1. 長さを揃えることができたら、一度マイコンを抜きとります。この時、ギリギリでカットしすぎたりニッパーの質が悪いと、ピンの先端が変形し、マイコンがなかなか基板から抜けない場合があります。その場合は破損しないように注意しながら引き抜いてください。

<a id="3-4-バッテリーコネクタの取り付け"></a>
### 3-4. バッテリーコネクタの取り付け

Lipoバッテリー用のコネクタを取り付けます。

1. バッテリーコネクタを任意の長さに切断します。長さは基本的に好みですが、長すぎてもケーブルの取り回しが難しくなることがあるので2~3センチメートル程度を推奨します。
2. ケーブルの被覆を2mmほど剥きます。ニッパーやカッターで剥けますが、ケーブルが細く慣れていないとケーブル自体を切断してしまうこともあるので、先程切ったケーブルの切れ端で練習してから挑むことをおすすめします。
![DSC00048](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00048.JPG)

3. 基板の裏面からバッテリー端子用のスルーホールにはんだ付けします。この時、BAT+に赤色、BAT-に黒色を接続します。必ず間違えないように確認してください。（ただし例外的に逆に配線する場合もあります。詳細は[2-2-1. バッテリーの選び方と注意点](#2-2-1-バッテリーの選び方と注意点)をいただき、極性に間違いの無いように配線を行ってください。）\
    バッテリーをマイコンカバーに格納する予定の方は画像の通り（基板下側向き）に、大容量ケースに格納する予定の方は逆方向（基板上側向き）にはんだ付けしたほうが少しだけケーブルが取り回しやすくなります。迷ったら画像の向きではんだ付けすればOKです。
    ![DSC00049](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00049.JPG)
    組み立て済の場合、すべて下向きではんだ付けしてあります。

ここで切り落としたコネクタの線は、使用するモデルによって後の[3-8. 使用モデルに応じた配線](#3-8-使用モデルに応じた配線)で使用する場合があります。捨てずに取っておいてください。

<a id="3-5-コンスルーの取り付け"></a>
### 3-5. コンスルーの取り付け

マイコンを装着するためのコンスルーピンを取り付けます。

1. Keyball基板のOLEDとPro Microを取り外します。キーキャップやキースイッチなども取り外しておいたほうが作業性がよくなります。
2. コンスルーピンをKeyball基板の表面に差し込みます。差し込む穴は画像を参照してください。特に左側は、本家KeyballでPro Microを差し込んでいた場所と異なりますので注意が必要です。\
  右トラボの場合
  ![DSC00414](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00414.JPG)
  左トラボの場合
  ![IMG_1064](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1064.jpg)
  ishの場合
  ![IMG_1065](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1065.jpg)
  また、この時コンスルーピンには正しい向きがありますので、[本家Keyballのビルドガイド](https://github.com/Yowkees/keyball/blob/main/keyball39/doc/rev1/buildguide_jp.md#3-6promicro%E3%81%AE%E3%81%AF%E3%82%93%E3%81%A0%E4%BB%98%E3%81%91)を参考に差し込む向きもご確認ください。
  ![DSC00054](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00054.JPG)

1. コンスルーピンを差し込んだら、その上からSeaSideXの基板を差し込みます。この時に、トラボ側基板ではんだ付けせずに残して置いたポゴピンの足が干渉し隙間が空きやすいので、色々な角度から隙間を覗き、コンスルーを基板の間に隙間がないことをしっかりとご確認ください。\
  下の画像の部分が特に隙間が空きやすいので注意。最悪隙間があっても動作に問題はないので、基板の傾きが気にならない方は神経質にならずに作業を進めてもOKです。
  ![DSC00062](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00062.JPG)


4. 隙間が無いことを確認したらコンスルーピンをはんだ付けして固定します。この時、はんだを盛りすぎるとマイコンを装着する際に干渉する場合があるので、少量のはんだで軽く接着するようなイメージではんだ付けを行ってください。\
  コンスルーピンははんだ付けしなくても電気的に導通するので、ポゴピンやマイコン用のスルーホールと干渉するリスクのあるピン（画像赤枠のあたり）については無理にはんだ付けをする必要はありません。あくまでコンスルーが抜けてしまわないように固定するためにはんだ付けを行いますので、最悪四隅のピンだけでもはんだ付けできていればOKです。
  ![DSC00058](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00058.JPG)



<a id="3-6-ポゴピン残りのはんだ付け（ボール側のみ）"></a>
### 3-6. ポゴピン残りのはんだ付け（ボール側のみ）

ボール側基板ではんだ付けせずに残して置いたポゴピンの足をはんだ付けします。

1. SeaSideX基板をKeyball基板から外します。
2. 右側基板裏側の、はんだ付けがされていないピンにはんだ付けをします。コンスルーが干渉しているので、溶かしてしまわないようにだけ注意しながら短時間の加熱・少量のはんだでさっとはんだ付けを行います。
![DSC00063](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00063.JPG)

<a id="3-7-マイコンのはんだ付け"></a>
### 3-7. マイコンのはんだ付け

Seeed XIAO BLE nRF52840を基板に取り付けます。

1. マイコンを基板のスルーホールに差し込みます。コンスルーがスルーホールに少し干渉しているので刺さりにくいことがありますが、慎重かつ力強く押し込むとなんとかなるはずです。もしかするとここが一番の難所かもしれません。
![DSC00064](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00064.JPG)
2. 差し込んだマイコンによってポゴピンの先端が押し込まれていることを確認します。
3. 差し込んだマイコンとSeaSideX基板が平行になるように傾きを微調整します。
![012153818](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/012153818.jpg)
4. 先ほどのポゴピンの足と同様に、こちらもコンスルーと干渉していますので溶かしてしまわないよう注意しつつ、さっとはんだ付けをします。
5. 画像のようになればOKです。
![DSC00065](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00065.JPG)
  マイコンの足をカットしなかった場合は以下のような仕上がりになります。
  ![232758465](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/232758465.jpg)

<a id="3-8-使用モデルに応じた配線"></a>
### 3-8. 使用モデルに応じた配線

`SeaSideX`を`SeaSide39`にするか`SeaSide44`にするかを選ぶ配線を行います。対象はボール側の基板のみです。\
左手トラボで使用する場合は少し事情が異なるので[3-8-3. SeaSide39(左手トラボ)用配線](#3-8-3-SeaSide39(左手トラボ)用配線)をよく読み配線を行ってください。

| モデル | 必要な配線 |
|:---|:---|
| Keyball39 | SeaSide39用配線 |
| Keyball44 | SeaSide44用配線 |
| Keyball39ish | SeaSide39用配線 |
| Keyball44ish | SeaSide44用配線 |
| Keyball39左トラボ | SeaSide39用配線+α |
| Keyball39ish左トラボ | SeaSide44用配線 |

<a id="3-8-1-SeaSide39用配線"></a>
#### 3-8-1. SeaSide39用配線

SeaSide39として使用する場合は、ボール側基板の39パッドをはんだでブリッジさせる必要があります。\
以下のようになればOKです。\
![IMG_1060](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1060.jpg)

<a id="3-8-2-SeaSide44用配線"></a>
#### 3-8-2. SeaSide44用配線

SeaSide44として使用する場合は少し難易度が上がりますが、ボール側基板の画像で示す2箇所をつなぐように配線する必要があります。\
一連の作業を動画にしたので参考にご覧ください。（終盤ピントが合ってないですが、雰囲気で感じ取ってください！）\
https://youtu.be/jyEgmNJrH-E

[3-4. バッテリーコネクタの取り付け](#3-4-バッテリーコネクタの取り付け)で取っておいたコネクタ線の切れ端を使用し、画像の長さの線を作成します。\
![IMG_1071](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1071.jpg)

被覆を剥く時はカッティングマットの上で軽くカッターを当ててケーブルを転がすように切るのがおすすめです。被覆を剥いた線に予備はんだをしておいてください。\
マイコン側にはんだ付けします。厳密には接続する対象は一番右下のパッドですが、SeaSideXの仕様だと上2つのパッドに接続されてしまっても動作上影響はないので、はんだ付けの難易度を下げる意味で右側３つのパッドすべてに同時にはんだ付けしてしまいます。\
先ほどの動画を参考に、コテ先にはんだを盛り、パッドに3mm剥いたほうの線を当てた状態で、軽く溶かすようにコテ先を当てて配線してください。\
マイコン側の配線ができたらピンセットなどで配線を整え、位置が決まったら基板44のパッド(スルーホール)にはんだ付けしてください。

以下のようになればOKです。\
![IMG_1072](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1072.jpg)

<a id="3-8-3-SeaSide39(左手トラボ)用配線"></a>
#### 3-8-3. SeaSide39(左手トラボ)用配線

先述の通り左手トラボで使用する場合は少し事情が異なります。

| モデル | 必要な配線 |
|:---|:---|
| Keyball39左トラボ | SeaSide39配線+α |
| Keyball39ish左トラボ | SeaSide44配線 |

Keyball39左トラボでは、先述の[SeaSide39用配線](#3-8-1-seaside39用配線)に加えて、Keyball39本体のボール側基板背面のLEFTパッドの短絡を外す必要があります。\
以下のようになればOKです。
![IMG_1059](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1059.jpg)
これにより、SeaSideから元のProMicroに戻したくなった時には再度このLEFTパッドを接続する必要がでてきます。KeyballとSeaSideで行き来する気軽さが少し減ってしまいますが、ご了承いただけますと幸いです。

Keyball39ishの左トラボモデルの場合、39ではありますが先述の[SeaSide44用配線](#3-8-2-seaside44用配線)を行ってください。少し気持ち的な違和感があるかもしれませんが、こちらもご了承いただけますと幸いです。


<a id="3-9-トラックボールセンサーのはんだ付け"></a>
### 3-9. トラックボールセンサーのはんだ付け

省電力タイプのトラックボール読み取りセンサーを基板に取り付けます。

1. センサーを基板に差し込みます。画像を参考に、向きを間違えないようにしてください。
![DSC00072](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00072.JPG)
2. すべてのピンにはんだ付けをし、センサーの保護シールを剥がします。はんだ付けの際に、はんだごてが表面実装の部品に触れてしまわないよう注意してください。
![DSC00076](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00076.JPG)
3. センサー用レンズを差し込みます。画像を参考に、向きを間違えないようにしてください。
![DSC00077](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00077.JPG)

以上ではんだ付けは完了です。お疲れさまでした！\
スライドスイッチをオン（左側）に入れ、USBケーブルを繋ぐと充電インジケータが緑色に光り、充電されていることが確認できるはずです。バッテリーの充電はスイッチをオンにしている時にしか行われないのでご注意ください。

![DSC00067](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00067.JPG)


<a id="3-10-LED配線カット"></a>
### 3-10. LED配線カット

[1-6. LED配線によるバッテリー持続時間の違い](#1-6-led配線によるバッテリー持続時間の違い)で説明した通り、SeaSideXをLED配線を行っているKeyballで使用する場合、点灯していないLEDの待機電力によってバッテリー持ちが悪くなることが報告されています。\
しかし、本家Keyball基板に少し手を入れることでこちらを改善できますので、バッテリー持ちが気になる場合は以下の手順を実施してください。

本家Keball基板の裏面にある「LED CUT」と書かれたパッドを探します。片側につき２箇所あります。
![1408](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1408.jpg)

パッドの真ん中をカッターなどでガリガリと削ります。（画像は削った後）\
これにより、LED配線が物理的に切断された相当の状態となります。
![1409](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1409.jpg)

もしLEDが恋しくなった時は、切断したパッドをはんだでブリッジさせることで元通りにすることも可能です。

<a id="3-11-組み立て"></a>
### 3-11. 組み立て

ここまでの作業でSeaSideXの主要部分の組み立ては完了しました。最後にKeyball基板への装着とカバーおよびケース（オプションパーツ）の取り付けを行います。購入されたパーツに応じて必要な作業だけを行ってください。\
39の写真が中心となりますがどのモデルも装着方法は同じですので適宜読み替えていただくようお願いいたします。また、ishシリーズは専用ケースを用意しておりません。カバーのみとなります。

作業中はSeaSideXのスイッチをオフ（右側）にしたままにしておいてください。

1. バッテリーコネクタの向きを確認します。大容量ケースを使用しない方は、コネクタケーブルを基板下側へ向け、大容量ケースを使用する方は基板上側に向けます。大容量ケースを使用する、かつ下向きにコネクタをはんだ付けした方は、画像のようにコネクタケーブルを曲げて基板上側に向けます。
  このとき、ケーブルの根本に負荷がかかると断線するおそれがあるので優しく取り扱ってください。
  ![DSC00456](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00456.JPG)
  
1. SeaSideXをKeyball基板に装着します。差し込む穴は画像の通りです。
  ishシリーズの場合は差し込める穴が一箇所だけのはずですので差し込める通りに差し込めばOKです。\
  Keyball39と44の場合
  ![DSC00414](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00414.JPG)
  Keyball39左トラボの場合 
  ![IMG_1064](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/IMG_1064.jpg)
  大容量ケースを使用しない方は、画像のようにOLED用のピンソケットを避けるように隙間を通してください。ソケットと基板でケーブルを挟みこんでしまわないように注意します。
  ![DSC00455](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00455.JPG)
  大容量ケースを使用する方は、Keyball39基板の底面側に出るようにケーブルを通してください。
  ![DSC00457](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00457.JPG)

1. バッテリーを装着します。  大容量ケースを使用しない方は、マイコンカバーの裏面に両面テープで200mAhバッテリーを固定しコネクタを接続します。画像を参考に、組み立てた時にXIAO BLEと干渉しないように位置決めをしてください。
  ![DSC00458](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00458.JPG)
  ケーブルがはみ出さないように注意しつつ、隙間に押し込みながらカバーをネジ止めします。
  ![DSC00459](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00459.JPG)
  写真のようにUSBコネクタとカバーの位置が合っていればOKです。
  ![DSC00460](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00460.JPG)
  大容量ケースを使用する方は、バッテリーを接続する前にケースを装着する必要があります。画像のようにコネクタを穴から下に出し、赤く囲ったネジだけ（右側2箇所、左側1箇所）を固定します。
  ![DSC00461](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00461.JPG)
  大容量ケースの底面パーツにバッテリーを両面テープで固定し、コネクタを接続します。
  ![DSC00462](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00462.JPG)
  ケーブルがはみ出さないように注意しつつ、隙間に押し込みながらカバーを閉じます。
  ![DSC00463](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00463.JPG)
  残りのネジを締めます。底面パーツのネジ止めは、大容量ケースに付属の8mmネジを使用します。写真のように隙間が空いていなければOKです。
  ![DSC00464](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00464.JPG)
  専用ケースおよび大容量ケースどちらの場合も、画像のようにコネクタとスイッチが位置がケースに合っていることを確認してください。
  ![DSC00441](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00441.JPG)

1. トラックボール読み取り基板を元のKeyballのものからSeaSideXのものに置き換えます。Keyballのものとほぼ同じサイズになっているので、元の状態と同じように基板を差し替えるだけでOKです。
![DSC00077](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/DSC00077.JPG)
1. 基板の差し替えが済んだら、トラックボールケースを元通りに装着しケースに固定します。

<a id="4-ファームウェア"></a>
## 4. ファームウェア

<a id="4-1-テスト用ファームウェアのダウンロード"></a>
### 4-1. テスト用ファームウェアのダウンロード

まずはテスト用のファームウェアを書き込み、動作確認を行います。\
ファームウェアは使用するモデルごとに異なりますので、以下のリンクからファームウェアを選択しダウンロードしてください。

| モデル | リンク |
|:-|:-|
| Keyball39右トラボ | [ダウンロード](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/test_firmware/SeaSide39_firmware.zip) |
| Keyball39左トラボ | [ダウンロード](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/test_firmware/SeaSide39_leftball_firmware.zip) |
| Keyball39ish右トラボ | [ダウンロード](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/test_firmware/SeaSide39ish_firmware.zip) |
| Keyball39ish左トラボ | [ダウンロード](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/test_firmware/SeaSide39ish_leftball_firmware.zip) |
| Keyball44右トラボ | [ダウンロード](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/test_firmware/SeaSide44_firmware.zip) |
| Keyball44ish右トラボ | [ダウンロード](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/test_firmware/SeaSide44ish_firmware.zip) |

ダウンロード後zipファイルを展開し、
- `SeaSideXX_L rgbled_adapter-seeeduino_xiao_ble-zmk.uf2`
- `SeaSideXX_R rgbled_adapter-seeeduino_xiao_ble-zmk.uf2`
- `settings_reset-seeeduino_xiao_ble-zmk.uf2`

という３つのファイルが入っていることを確認してください。(XXは39または44)

<a id="4-2-テスト用ファームウェアの書き込みとペアリング"></a>
### 4-2. テスト用ファームウェアの書き込みとペアリング

マイコンにファームウェアを書き込みます。テスト用といいつつ通常動作するファームウェアなので、この工程が済むと一旦の完成になります。（キーマップは確認用の適当なものです。）\
おそらく今後自分だけのファームウェア設定を模索していくことになると思います。テスト用ではない本番のファームウェアはぜひ皆さんの手で作り上げてください。

1. SeaSideXのスイッチがオフ（右側）になっていることを確認します。
2. マイコンをブートローダーモードにします。
   - PCとSeaSideX（NoBallSide）をUSBケーブルで接続します。
   - マイコンのリセットボタンを素早く2回押します。専用カバーの場合、ふたつ空いているうちに左側がリセットスイッチ用の穴です。爪楊枝などで押し込んでください。ボタンが小さいので穴越しに2回押すのは最初少し難しいかもしれません。（何回かやればすぐ慣れます）
   - PC上で「XIAO SENSE」というドライブが認識されれば成功です。
3. 「XIAO SENSE」ドライブに `settings_reset-seeeduino_xiao_ble-zmk.uf2` をドラッグ&ドロップまたはコピー&ペーストで書き込みます。この時、macの場合画像のようなメッセージが出る場合がありますが、「XIAO SENSE」ドライブが自動的に認識されなくなっていたら書き込みに成功しています。\
   `settings_reset-seeeduino_xiao_ble-zmk.uf2` は設定初期化用のファイルなので、基本的に以後ファームウェアの書き換えを行う際などには書き込み不要です。
  ![err1](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/err1.png)
1. 再度マイコンをブートローダーモードにし、今度はNoBallSide用のファームウェア(右手トラボの場合 `SeaSideXX_L rgbled_adapter-seeeduino_xiao_ble-zmk.uf2`, 左手トラボの場合`SeaSideXX_R rgbled_adapter-seeeduino_xiao_ble-zmk.uf2`) を同様の手順で書き込みます。この時も同様のメッセージが出ることがありますが、正常です。
2. SeaSideX(BallSide)の右側にも同様の手順で`settings_reset-seeeduino_xiao_ble-zmk.uf2` → 先ほどと逆のファームウェアファイル の順番で書き込みを行います。
3. 左右の書き込みが完了したらUSBケーブルを取り外し、両方のSeaSideXのスイッチをオン（左側）にし、マイコンのリセットスイッチをNoBallSide→BallSideの順番で一度ずつ押します
4. 電源オンの時やリセットの時にマイコンのLEDが点滅するはずです。専用カバーの場合右側の穴がLED確認用の穴です。以下の意味がありますので、正常に点滅することを確認してください。
   - 最初の点灯（バッテリーの残量）
     - 🟢/🟡/🔴の三段階で点灯。SeaSideXの場合は40%以上は🟢、20%までは🟡、それ以下は🔴が点灯するように設定されています。
     - この閾値はファームウェアを編集することでお好みに設定できます。
   - 2つ目の点灯（ブルートゥースの接続状況）
      - 🔵は接続成功、🟡はペアリング中、🔴は接続失敗を意味します。
      - 左右で少し意味が異なり、左側の点灯は親側（右側）へのペアリング状況を意味し、右側の点灯はPCなどの機器へのペアリング状況を意味します。
  - ですので、ファームウェア書き込み後の正常な点灯は以下のとおりです。
    - NoBallSide：🟢/🟡/🔴（バッテリーの充電状況次第）→ 🔵（ BallSideとの接続成功）
    - BallSide：🟢/🟡/🔴（バッテリーの充電状況次第）→ 🟡（P機器とのペアリング中）
  
  詳細は[zmk-rgbled-widget](https://github.com/caksoylar/zmk-rgbled-widget)のREADMEをご覧ください。
8. 正常に点灯していたらPC側でBluetoothデバイスとして「SeaSide39」や「SeaSide44ish」などが認識されているはずです。接続を行ってください。

<a id="4-3-動作確認"></a>
### 4-3. 動作確認

Bluetoothの接続後、キーやトラックボールの動作を確認してください。\
初回起動時、稀にトラックボールが一時的に反応しないことがあります。電源をいれたまま10分ほど待ってみて、反応がなければリセットスイッチや電源のオンオフ、トラックボール読み取り基板の抜き差しなどを試してみてください。それでもトラックボールが反応しない場合は組み立てのミスやセンサーの故障が疑われますので、ご連絡いただけますと可能な範囲でサポートいたします。（注意事項にも記載したとおり、すべてにサポートしきれない可能性があることはご了承ください。）

<a id="4-4-zmk-studioの活用"></a>
### 4-4. ZMK Studioの活用

[注意事項](#1-3-zmkファームウェアの使用)で説明したとおり、ZMK Studioを使用することでファームウェアを書き換えることなくGUIでキーマップを簡単に編集できます。\
Remapなどに近い操作感で設定が可能ですが、機能に一部制限があります。そもそもまだ開発段階？のようです。なのでZMK Studioでのカスタマイズのみでは後々物足りなくなる可能性が高いですが、GitHubに慣れていない方などはまずはこちらでいろいろ触ってみるのも手だと思います。

1. [ZMK Studio](https://zmk.studio/)にアクセスします。
2. 接続するキーボードを選択します。
3. 接続が完了すると、現在のキーマップが表示されます。
4. 変更したいキーをクリックし、任意の動作を選択します。
5. 設定が完了したら右上の保存ボタンをクリックして変更を保存します。
   
細かい操作や設定、どういった制限があるのかなどについてはここでは説明しませんので詳しくは[こちら](http://zmk.dev/docs/features/studio)を参照してください。

<a id="4-5-zmkファームウェアのカスタマイズとビルド方法"></a>
### 4-5. ZMKファームウェアのカスタマイズとビルド方法

ZMK Studioで対応していない高度な設定を行いたい場合は、直接ファームウェアをカスタマイズしてビルドする必要があります。ファームウェアのカスタマイズビルドにはGitHubを使用します。\
おおまかなフローは以下のとおりです。ここでは各ツールの細かな使い方の説明はしませんので、必要に応じて調べてみてください。
![flow](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/flow.jpg)

使用するファームウェアのリポジトリはモデルによって異なります。間違えないに選択してください。

| モデル | リポジトリ |
|:-|:-|
| Keyball39右トラボ | https://github.com/hama-be/zmk-config-SeaSide39 |
| Keyball39左トラボ | https://github.com/hama-be/zmk-config-SeaSide39-leftball |
| Keyball39ish右トラボ | https://github.com/hama-be/zmk-config-SeaSide39ish |
| Keyball39ish左トラボ | https://github.com/hama-be/zmk-config-SeaSide39ish-leftball |
| Keyball44右トラボ | https://github.com/hama-be/zmk-config-SeaSide44 |
| Keyball44ish右トラボ | https://github.com/hama-be/zmk-config-SeaSide44ish |
| 初期ロットSeaSide39 | https://github.com/hama-be/zmk-config-SeaSide39-old |

1. 上の表から選択したファームウェアをフォークする
  - あなたのGitHubアカウント上に該当のリポジトリが表示されていればOKです。
2. 手動またはKeymapEditorでファームウェアを編集する
  - [ZMK Keymap Editor](https://nickcoutsos.github.io/keymap-editor/) とあなたのGitHubアカウントを接続すると、KeymapEditorから直接リポジトリへ変更をプッシュすることができます。
  - キーマップ以外の各種設定値などを変更する場合はファイルを直接編集しプッシュしてください。好みに応じて編集するであろう設定は以下の箇所です。特にオートマウスレイヤを使用するかどうかは非常に好みの分かれるところなのではないでしょうか。
    - `config/boards/shields/SeaSide39/SeaSide39_R.conf`
    ```
    # トラックボールの感度設定（値が高いほど感度が高くなる）
    CONFIG_PMW3610_CPI=600
    # オートマウスレイヤー有効時、マウスレイヤーが無効化されるまでの時間（ミリ秒）
    CONFIG_PMW3610_AUTOMOUSE_TIMEOUT_MS=600

    # 電源オン時のLEDインジケータの有効/無効
    CONFIG_RGBLED_WIDGET=y 
    # バッテリー残量が40%未満の時黄色、20%未満の時赤色表
    CONFIG_RGBLED_WIDGET_BATTERY_LEVEL_HIGH=40    
    CONFIG_RGBLED_WIDGET_BATTERY_LEVEL_CRITICAL=20 

    # レイヤー切り替え時のLEDインジケータの有効/無効
    CONFIG_RGBLED_WIDGET_SHOW_LAYER_COLORS=y

    # レイヤーごとの色設定（0=オフ, 1=赤, 2=緑, 3=黄, 4=青, 5=マゼンタ, 6=シアン, 7=白
    # オートマウスレイヤーだけ青色に光り、それ以外のレイヤーはオフに設定
    CONFIG_RGBLED_WIDGET_LAYER_0_COLOR=0
    CONFIG_RGBLED_WIDGET_LAYER_1_COLOR=0
    CONFIG_RGBLED_WIDGET_LAYER_2_COLOR=0
    CONFIG_RGBLED_WIDGET_LAYER_3_COLOR=0
    CONFIG_RGBLED_WIDGET_LAYER_4_COLOR=4
    CONFIG_RGBLED_WIDGET_LAYER_5_COLOR=0
    CONFIG_RGBLED_WIDGET_LAYER_6_COLOR=0
    CONFIG_RGBLED_WIDGET_LAYER_7_COLOR=0
    ```    
  - `config/boards/shields/SeaSide39/SeaSide39_R.overlay`
    ```
    trackball: trackball@0 {
        status = "okay";
        compatible = "pixart,pmw3610";
        reg = <0>;
        spi-max-frequency = <2000000>;
        irq-gpios = <&gpio0 2 (GPIO_ACTIVE_LOW | GPIO_PULL_UP)>;
        automouse-layer = <4>; //ここをコメントアウトするとオートマウスレイヤーがオフになる
        scroll-layers = <5>; 
    };
    ```
3. ビルドされたファームウェアをダウンロードして書き込む
  - 「GitHub Actions」という機能を使って、コードをプッシュするたびに自動的にファームウェアがビルドされます。
  - Actionsはリポジトリの「Actions」タブから確認できます。初回は手動で有効化が必要です。
  - リポジトリに変更をプッシュすると数分でビルドが完了します。「Actions」タブから最新のワークフローを開き、Artifactsからファームウェアをダウンロードしてください。
    ![build](https://raw.githubusercontent.com/hama-be/SeaSideX-documentation/main/docs/img/build.png)
  - ダウンロードしたファームウェアを書き込みます。キーマップの変更の場合は右側だけの書き込みでOKです。


ZMKファームウェアについて、細かくカスタマイズをしたい方は[ZMK公式ドキュメント](https://zmk.dev/docs/)を参照してください。


 
<a id="5-お疲れさまでした"></a>
## 5. お疲れさまでした

これにて組み立ては完了です。お疲れさまでした！\
ぜひ使用感やご意見ご要望、便利なファームウェアやキーマップのセッティングなど、何でも良いので `#SeaSideX`, `#SeaSide39`, `#SeaSide44`などをつけて共有いただけると嬉しいです。見に行きます！\
それでは、良き無線Keyballライフをお過ごしください☺️