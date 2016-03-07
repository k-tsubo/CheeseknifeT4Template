# CheeseknifeT4Template

レイアウトのxmlファイルからCheeseknife用のコードの生成を行うT4テンプレート。
partialクラスとしてCheeseknife用のコードを出力します。

# 使い方

基本的にMainActivity.designer.ttをコピーして9行目を書き換えるのみ。
```
// レイアウトファイルをこのテンプレートからの相対パスで指定
var layoutFile = Host.ResolvePath("./Resources/Layout/Main.axml");
```

# 出力例

プロジェクトを作成した時に生成されるMain.axmlを指定すると、以下のように出力されます。

- レイアウトファイル
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <Button
        android:id="@+id/myButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/hello" />
</LinearLayout>
```

- 変換結果(MainActivity.designer.cs)
```
using Android.Views;
using Android.Widget;
using Com.Lilarcor.Cheeseknife;

namespace ChesseknifeT4Template
{
    public partial class MainActivity
    {
        [InjectView(Resource.Id.myButton)]
        private Button myButton;
    }
}
```

# 備考
- 変数名はandroid:idをlower camelに変換する
  - 変数名の出力ルールを変更する場合は51行目を変更する
```
private <#= className #> <#= ToLowerCamel(id) #>;

// UpperCamelにしたい場合は
private <#= className #> <#= ToUpperCamel(id) #>;
```
