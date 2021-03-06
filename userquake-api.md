# 地震感知情報API

**本APIの利用は推奨しません**

JSON APIの利用を推奨します。本APIは互換性のために残されており、地震情報の概要以外の情報を取得することはできません。

## 概要

地震感知情報APIでは，P2P地震情報ネットワーク上に配信された「地震情報」「津波予報（未実装）」「地震感知情報（提供停止中）」の取得が可能です。

APIは，文字コードにShift_JISを使用しています。

## 基本仕様

- URI: http://api.p2pquake.com/v1/userquake
- リクエストメソッド: GET

## サンプル

一部のヘッダ情報は省略しています。

```
> GET /v1/userquake?date=2016/09/07 HTTP/1.1

< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=Shift_JIS
<
< 00:26:19,QUA,07日00時22分/3/2/1//ごく浅い/-1.0/0///気象庁
< 00:27:20,QUA,07日00時22分/3以上/0/2/宮古島近海/50km/4.8/0/N24.8/E125.3/
< 00:29:23,QUA,07日00時22分/3/0/4/宮古島近海/50km/4.8/0/N24.8/E125.3/
< 01:59:35,QUA,07日01時56分/3以上/0/2/熊本県熊本地方/10km/3.8/0/N32.7/E130.6/
< 02:00:28,QUA,07日01時56分/4/0/4/熊本県熊本地方/10km/3.8/0/N32.7/E130.6/
< 02:19:31,QUA,07日02時14分/1/0/4/熊本県熊本地方/10km/2.2/0/N32.7/E130.6/
< 02:24:33,QUA,07日02時19分/1/0/4/種子島近海/30km/3.8/0/N30.6/E131.2/
```

## パラメタ

フィールド名|必須|内容
--|--|--
date|yes|日付 (mm/ddまたはyyyy/mm/dd形式)

## レスポンス

レスポンスはテキストデータで，レコードはCRLFで区切られています。

レコードはカンマ区切りで分割でき，それぞれ「時刻」「情報コード」「詳細情報」となります。

```
01:59:35,QUA,07日01時56分/3以上/0/2/熊本県熊本地方/10km/3.8/0/N32.7/E130.6/
```

### 地震情報

情報コード `QUA` が地震情報です。

```
01:59:35,QUA,07日01時56分/3以上/0/2/熊本県熊本地方/10km/3.8/0/N32.7/E130.6/
```

詳細情報はスラッシュで分割でき，「発生日時」「震度」「津波の有無（0=なし,1=あり,2=調査中,3=不明）」「地震情報種類（1=震度速報,2=震源情報,3=震源・震度情報,4=震源・詳細震度情報,5=遠地地震情報）」「震源」「深さ」「マグニチュード」「震度訂正(0=いいえ,1=はい)」「緯度(N=北緯,S=南緯)」「経度(E=東経,W=西経)」「発表管区」となります。

## 補足事項

- リクエスト数が過大とならないよう配慮をお願いします。
- IPアドレス単位でおよそ 30リクエスト/分 を超える場合，アクセスを制限する可能性があります。