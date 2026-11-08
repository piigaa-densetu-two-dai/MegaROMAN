～～～ メガロマン ～～～

〇はじめに

メガロマンは最大容量16368KB、SCC音声出力対応のMSX用メガロムカートリッジです。MSXπのメガロム機能専用バージョンみたいなものです。
どちらかというと都度書き換えて使うような使い方より書き換えないで使い続ける感じの使い方を想定しています。

〇対応マッパー

* ASCII 8Kマッパー(ROM容量2048KB)
* ASCII 16Kマッパー(ROM容量4096KB)
* ASCII 16X(16M版)マッパー(ROM容量16368KB、ROM領域リードオンリー(自己書換機能無し))
* ASCII 16X(8M版)マッパー(ROM容量8192KB、ROM領域リードオンリー(自己書換機能無し)) 8192KB以下のROM用
* KONAMIマッパー(ROM容量2048KB)
* KONAMI SCCマッパー(ROM容量2048KB、SCC音声出力対応)

ファームウェアは各マッパー毎に異なります。

〇各マッパー詳細

* ASCII 8Kマッパー(ROM容量2048KB)

ファームウェア
MegaROMAN_ASCII8K.bin

ROMページ
0 0x4000-0x5fff
1 0x6000-0x7fff
2 0x8000-0x9fff
3 0xa000-0xbfff

ROMバンク切替アドレス範囲
0 0x6000-0x67ff, 0xe000-0xe7ff 初期値0
1 0x6800-0x6fff, 0xe800-0xefff 初期値0
2 0x7000-0x77ff, 0xf000-0xf7ff 初期値0
3 0x7800-0x7fff, 0xf800-0xffff 初期値0(但しシステム起動時にランダム値に変化する場合有り)

* ASCII 16Kマッパー(ROM容量4096KB)

ファームウェア
MegaROMAN_ASCII16K.bin

ROMページ
0 0x4000-0x7fff
1 0x8000-0xbfff

ROMバンク切替アドレス範囲
0 0x6000-0x67ff, 0xe000-0xe7ff 初期値0
1 0x7000-0x77ff, 0xf000-0xf7ff 初期値0

* ASCII 16Xマッパー(ROM容量16368KB、ROM領域リードオンリー(自己書換機能無し))

ファームウェア
MegaROMAN_ASCII16X.bin

ROMページ
0 0x4000-0x7fff
1 0x8000-0xbfff

ROMバンク切替アドレス範囲
0 0x6000-0x6fff, 0x2000-0x2fff, 0xa000-0xafff, 0xe000-0xefff 初期値0
1 0x7000-0x7fff, 0x3000-0x3fff, 0xb000-0xbfff, 0xf000-0xffff 初期値0(但しシステム起動時にランダム値に変化する場合有り)

* ASCII 16Xマッパー(ROM容量8192KB、ROM領域リードオンリー(自己書換機能無し))

ファームウェア
MegaROMAN_ASCII16X_8M.bin

ROMページ
0 0x4000-0x7fff
1 0x8000-0xbfff

ROMバンク切替アドレス範囲
0 0x6000-0x6fff, 0x2000-0x2fff, 0xa000-0xafff, 0xe000-0xefff 初期値0
1 0x7000-0x7fff, 0x3000-0x3fff, 0xb000-0xbfff, 0xf000-0xffff 初期値0(但しシステム起動時にランダム値に変化する場合有り)

* KONAMIマッパー(ROM容量2048KB)

ファームウェア
MegaROMAN_KONAMI.bin

ROMページ
0 0x4000-0x5fff
1 0x6000-0x7fff
2 0x8000-0x9fff
3 0xa000-0xbfff

ROMバンク切替アドレス範囲(オリジナルより範囲が狭いです)
0 固定バンク変更不可 初期値0
1 0x6000-0x6fff, 0xe000-0xefff 初期値1
2 0x8000-0x8fff, 0x0000-0x0fff 初期値2
3 0xa000-0xafff, 0x2000-0x2fff 初期値3

* KONAMI SCCマッパー(ROM容量2048KB、SCC音声出力対応)

ファームウェア
MegaROMAN_SCC.bin

ROMページ
0 0x4000-0x5fff
1 0x6000-0x7fff
2 0x8000-0x9fff
3 0xa000-0xbfff

ROMバンク切替アドレス範囲
0 0x5000-0x57ff, 0xd000-0xd7ff 初期値0
1 0x7000-0x77ff, 0xf000-0xf7ff 初期値1
2 0x9000-0x97ff, 0x1000-0x17ff 初期値2
3 0xb000-0xb7ff, 0x3000-0x37ff 初期値3

SCCレジスターアドレス範囲(オリジナルと違って常時有効、書き込みオンリー・リード不可です)
0x9800-0x9fff, 0x1800-0x1fff 初期値オール0

〇使用法

1. 上記ファームウェアファイルの後ろに使用するROMファイル(対応マッパーのもの)を連結します。

unixのcatコマンドを使用する例
$ cat MegaROMAN_ASCII8K.bin game.rom > firmware.bin

windowsのcopyコマンドを使用する例
>copy /b MegaROMAN_ASCII8K.bin + game.rom firmware.bin

お手持ちのROMファイルはマッパー形式が変換されている場合があります。
動かない場合はblueMSX等でマッパーの確認をしてください。

2. uf2conv.exeを用いて1で作成したfirmware.binをuf2ファイルに変換します。

例: windowsコマンドプロンプト上で
uf2conv.exe firmware.bin firmware.uf2

uf2conv.exeはhttps://github.com/piigaa-densetu-two-dai/MSXpiにあります。

3. MSXに刺さっていない状態のメガロマンをブートモードでPCに接続します。

メガロマン裏面の穴から見えるBOOTSELボタンを押しながらPCとUSB接続して下さい。
接続が成功するとドライブが認識されます。

4. メガロマンに2で作成したfirmware.uf2ファイルを書き込みします。

3で認識されたドライブにfirmware.uf2をドラッグアンドドロップ(コピー)します。
コピーが完了するとドライブが見えなくなります。

5. 書込みが終わったらPCから外して完了

〇ASCII 16Xマッパーのコツ

8192KB以下のASCII 16XマッパーのROMファイル(ASTEROIDS/NeonHorizon_v1.0等)を使用する場合はMegaROMAN_ASCII16X_8M.binを使ってください。
NeonHorizon_v1.0のROMファイルを使用する場合はROMファイルのファイルオフセット0x2b1の0xc8を0xc9に書き換えて下さい。(自己書換チェックをスキップ)

〇注意

回路を簡素にする為に信号電圧レベル変換回路を省略しています。
RP2040のIOピン(プラス側にダイオードが入っていないピンのみ)をスロット端子に直結しています。
実質的に問題ないであろう事を確認していますが定格外の使い方をしているのでその辺自己責任でお願いします。

〇ライセンス

禁止事項

* メガロマンのファームウェア又は基板を盗用する事、名称、作者、配布元を偽る事、隠蔽する事(別の作品でやられました)
* メガロマンのファームウェア又は基板を使用した物品を販売する事、頒布と称する販売をする事
* メガロマンのファームウェア又は基板を使用した物品の組み立て作業を有償で行なう事
* カートリッジケース等の関連商品の販売を目的としたメガロマンの譲渡(有償・無償問わず)
* カートリッジケース等の関連商品の販売を目的としたメガロマンの組み立て作業の代行(有償・無償問わず)

ROMソフトウェアを提供する用途(主役がROMソフトウェアである場合)であればこの限りではありませんので私に聞いてください。
