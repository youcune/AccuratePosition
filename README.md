# AccuratePosition

1. navigator.geolocation.getCurrentPosition を使うと精度が低くても successCallback が呼ばれる
2. じゃあ navigator.geolocation.watchPosition を使えばええやん
3. でもそれだと一定以上の精度にならないときは止まってしまう
4. 一定以上の精度にならないならタイムアウトを設けてできるだけいい精度で取得するようにしよう

ということが簡単にできます。

## 使用例

```javascript
getAccuratePosition(
    function(position){
        alert('成功');
    },
    function(error){
        alert('失敗：' + error.message + '(' + error.code + ')');
    },
    {limit:200, timeout:4000}
);
```

動作としては「精度がlimitより良くなるまで取得し続けるけれど、timeout以上かかるようならやめてそれなりの精度の位置情報を取得する」です。 navigator.geolocation.getCurrentPosition とやってるところを getAccuratePosition に変えるだけで大丈夫そうです。

## オプション

使えるオプションは、

* limit: 許される誤差（m）。省略時は100。
* timeout: 待てる時間（ms）。省略時は無限。

のみです。

## 参考文献

* [geolocationでの位置情報取得 - teguのTech Blog](http://d.hatena.ne.jp/toshifumi_tegu/20100322/1269257133)
* [位置情報サービスのはじめ方：第3回　位置情報を取得してみよう（後編）｜gihyo.jp … 技術評論社](http://gihyo.jp/dev/feature/01/location-based-services/0003)

