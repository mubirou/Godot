# Godot Study Notes<a id="TOP"></a>

### <b>index</b>

[GDScript基礎文法](https://github.com/mubirou/HelloWorld/blob/master/languages/GDScript/GDScript_reference.md#gdscript-%E5%9F%BA%E7%A4%8E%E6%96%87%E6%B3%95) | [C#基礎文法](https://github.com/mubirou/HelloWorld/blob/master/languages/C%23Godot/C%23Godot_reference.md#c-with-godot-%E5%9F%BA%E7%A4%8E%E6%96%87%E6%B3%95) | [外部スクリプトエディタ](#外部スクリプトエディタ) | [Androidビルド](#Androidビルド) | [プリミティブ](#プリミティブ) | [カメラ](#カメラ) | [ノードの移動](#ノードの移動) | [マウス座標](#マウス座標) | [画面サイズ](#画面サイズ) | [背景色](#背景色) | [Rouletteゲーム](#Rouletteゲーム) | [SwipeCarゲーム](#SwipeCarゲーム) | [Quest + Oculus Link](#220501) | [Questコントローラー表示](#220502) | [is_button_pressed()](#220503) | [追跡](#220504) | [Questビルド](#220505) | [オブジェクト色](#220506) | [床タイル](#220507) | [RayCastボタン](#220601) |
***

<a id="外部スクリプトエディタ"></a>
# <b>外部スクリプトエディタ</b>

1. Godot の設定
    1. [エディター]-[エディター設定]-[Text Editor]-[External] を開く
    1. 次の通り設定  
        * [Use External Editor] : ✔
        * Exec Path] : C:/Users/XXXXX/AppData/Local/Programs/Microsoft VS Code/**Code.exe**  

1. Visual Studio Code の設定  
    1. VSCode を起動
    1. [表示]-[外観]-[アクティビティバーを表示する]
    1. 左側アイコンの一番下を選択
    1. [Marketplaceで機能拡張を検索] で **Godot** を検索
    1. **godot-tolls** をインストール

* Visual Studo Code ショートカットキー

    |Key|内容|
    |:--|:--|
    |Alt|上部メニューの表示/非表示|
    |Control + B|左サイドバーの表示/非表示|
    |Control + `|ターミナルの表示/非表示|
    |Control + `|ターミナルの表示/非表示|e
  
実行環境：Ubuntu 20.04 LTS、Godot 3.4.2、VSCode 1.63.2  
作成者：夢寐郎  
作成日：2021年12月30日  
[[TOP]](#TOP)


<a id="Androidビルド"></a>
# <b>Androidビルド</b>

* 既にビルドを試みて問題が生じている場合は先ず以下の作業を行う [[参考サイト](https://godotengine.org/qa/111977/apksigner-returned-with-error-%231)]  
  * Android Studio のアンインストール  
  * JDKフォルダの削除
  * .keystore ファイルの削除  

1. [Godot]-[プロジェクト]-[Androidビルドテンプレートのインストール]  
  [[参考サイト](https://qiita.com/2dgames_jp/items/3d0a318d2a483ced9db1)]

1. **Android Studio** (2020.3.1) のインストール  
  （注意）Android SDK ツールではない  
  https://developer.android.com/studio?hl=ja&gclid=EAIaIQobChMI4bb4moON9QIVTkNgCh14cABREAAYASAAEgKsUvD_BwE&gclsrc=aw.ds  
  C:\Program Files\Android\Android Studio にインストール

1. **OpenJDK** をインストール  
  ➊ ダウンロード  
  https://www.openlogic.com/openjdk-downloads?field_java_parent_version_target_id=416&field_operating_system_target_id=436&field_architecture_target_id=391&field_java_package_target_id=396  
  JAVA VERSION : **8u262-b10**（Java 11ではない）  
  DOWNLOAD : .zip  
  ➋ 解凍(今回は C:\OpenJDK とする)  
  ➌ binフィルダを開く  
  ➍ アドレス上で cmd と入力（コマンドプロンプトが開く）  
  ➎ keytool コマンドを実行  
  C:\OpenJDK\openlogic-openjdk-8u262-b10-win-64\bin>**keytool -keyalg RSA -genkeypair -alias androiddebugkey -keypass android -keystore debug.keystore -storepass android -dname "CN=Android Debug,O=Android,C=US" -validity 9999 -deststoretype pkcs12**  
  ➏ C:\OpenJDK\openlogic-openjdk-8u262-b10-win-64\bin> フォルダに **debug.keystore** が生成されたことを確認  
  [[参考サイト](https://godotengine.org/qa/111977/apksigner-returned-with-error-%231)]

1. Godot（エディター）の設定  
  ➊ [エディター]-[エディター設定]-[Export]-[Android] を下記の通り設定  
  ・Android Sdk Path : C:/Users/XXXXX/AppData/Local/Android/**Sdk**（手打ち）  
  ・Debug Keystore : C:/Users/XXXXX/Desktop/openlogic-openjdk-8u262-b10-windows-x64/openlogic-openjdk-8u262-b10-win-64/bin/**debug.keystore**（上記➏と同じ）  
  ・Debug Keystore User : **androiddebugkey**  
  ・Debug Keystore Pass : **android**  
  [[参考サイト](https://godotengine.org/qa/111977/apksigner-returned-with-error-%231)]

1. **.apk** エクスポート  
  ➊ [プロジェクト]-[エクスポート]-[追加]-[Android]  
  ➋ エクスポート先のパス : ……/XXXXX.apk  
  ➌ [Cumtom Template] を次の通りに設定  
  ・Debug : C:/Users/XXXXX/AppData/Roaming/Godot/templates/3.4.2.stable.mono/**android_debug.apk**（手打ち）  
  ・Release : C:/Users/XXXXX/AppData/Roaming/Godot/templates/3.4.2.stable.mono/**android_release.apk**  
   [プロジェクトのエクスポート] を選択 → [ファイルを保存]-[保存]

1. スマホの開発者向け設定  
  ➊ [設定]-[デバイス情報]-[すべての仕様]-[MIMUバージョン] を8回連打  
  ➋ [設定]-[追加設定]-[開発者向けオプション]-[USBデバッグ]と[USB経由でインストール] を ON  
  ➌ [✓私は起こりうるリスクを認識し、その結果として起こりうる結果を自発的に受け入れます]-[OK]  

1. スマホと PC を接続  
  ➊ USB ケーブルで接続  
  ➋ [ファイル転送/Android Auto] を ✓  

1. アプリのインストール  
  ➊ スマホの任意のフォルダに上記で作成した XXXXX.apk をコピー  
  ➋ スマホ上で XXXXX.apk を選択してインストール

実行環境：Windows 10、Godot 3.4.2、Xiaomi Redmi Note 9T (Android 11)  
作成者：夢寐郎  
作成日：2021年12月31日  
[[TOP]](#TOP)  


<a id="プリミティブ"></a>
# <b>プリミティブ</b>

1. [シーン]タブ-[+]で"**MeshInstance**"を検索し[作成]
1. [インスペクタ]-[Mesh]を以下の中から選択
  * ArrayMesh（？）
  * CapsuleMesh（カプセル＝物理挙動テスト）
  * CubeMesh（立方体＝壁･柱･箱･階段）
  * CylinderMesh（円柱）
  * PlaneMesh（平面）
  * PointMesh（点？）
  * PrismMesh（プリズム＝三角柱）
  * QuadMesh（画像表示･動画再生用）
  * SphereMesh（球＝星･弾丸）

実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年02月28日  
[[TOP]](#TOP)


<a id="カメラ"></a>
# <b>カメラ</b>

1. [シーン]タブ-[+]で"**Camera**"を検索し[作成]
1. [インスペクタ]で各種設定  

参考：[Hatena Blog](https://ore2wakaru2.hatenablog.com/entry/2018/03/04/232635)  
実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年02月28日  
[[TOP]](#TOP)


<a id="ノードの移動"></a>
# <b>ノードの移動</b>

### 【GDScript版】 

* [Spatialノード](https://docs.godotengine.org/ja/stable/tutorials/3d/introduction_to_3d.html#spatial-node)（3Dモデル）の移動  
  ```gdscript
  #Main.gd
  extends Spatial # 2Dの場合はNode2D

  var _ufo

  func _ready(): # 最初に一度だけ実行される
    _ufo = get_node("UFO")

  func _process(_delta): # 繰り返し実行
    _ufo.translation.y += 0.01 # 0.01m移動
  ```
  上記を含め次の方法で可能  
  ```gdscript
  # 指定位置に移動➀
  _ufo.translation.y += 0.01
  _ufo.translation += Vector3(0, 0.01, 0)

  # 指定位置に移動➁
  _ufo.transform.origin.y += 0.01
  _ufo.transform.origin += Vector3(0, 0.01, 0)

  # 指定した値だけ移動
  _ufo.translate(Vector3(0, 0.01, 0)) # Scaleに依存
  ```

* [Node2D](https://docs.godotengine.org/ja/stable/classes/class_node2d.html#node2d)ノード（2Dスプライト）の移動
  ```gdscript
  # Main.gd
  extends Node2D

  var _ufo

  func _ready(): # 最初に一度だけ実行される
    _ufo = get_node("UFO")
    
  func _process(_delta): # 繰り返し実行
    _ufo.position.x += 1 # 1ピクセル移動
  ```
  上記を含め次の方法で可能
  ```gdscript
  # 指定位置に移動
  _ufo.position.x += 1
  _ufo.position += Vector2(1, 0)
	
	# 指定した値だけ移動
  ufo.translate(Vector2(1, 0))
  ```

### 【C#版】 
* [Spatialノード](https://docs.godotengine.org/ja/stable/tutorials/3d/introduction_to_3d.html#spatial-node)（3Dモデル）の移動  
  ```c#
  // Main.cs
  using Godot;

  public class Main : Spatial {
    private Spatial _ufo;
    
    // 最初に一度だけ実行される
    public override void _Ready() {
      _ufo = GetNode("UFO") as Spatial;
      GD.Print(_ufo.Translation.y);
    }

    // 繰り返し実行される
    public override void _Process(float _delta) {
      Vector3 _ufoPos =  _ufo.Translation;
      _ufoPos.y += 0.01f;
      _ufo.Translation = _ufoPos;
    }
  }
  ```
  上記を含め次の方法で可能  
  ```c#
  // 指定位置に移動➀
  Vector3 _ufoPos =  _ufo.Translation;
  _ufoPos.y += 0.01f;
  _ufo.Translation = _ufoPos;

  // 指定位置に移動➁
  _ufo.Translation += new Vector3(0f, 0.01f, 0f);

  // 指定した値だけ移動（Scaleに依存）
  _ufo.Translate(new Vector3(0f, 0.01f, 0f));
  ```

* [Node2D](https://docs.godotengine.org/ja/stable/classes/class_node2d.html#node2d)ノード（2Dスプライト）の移動
  ```c#
  // Main.cs
  using Godot;

  public class Main : Node2D {
    private Node2D _ufo;

    // 最初に一度だけ実行される
    public override void _Ready() {
      _ufo = GetNode("UFO") as Node2D;
    }
    
    // 繰り返し実行される
    public override void _Process(float _delta) {
      Vector2 _ufoPos = _ufo.Position;
      _ufoPos.x += 1; // 1ピクセル移動
      _ufo.Position = _ufoPos;
    }
  }
  ```
  上記を含め次の方法で可能  
  ```c#
  // 指定位置に移動➀
  Vector2 _ufoPos = _ufo.Position;
  _ufoPos.x += 1; // 1ピクセル移動
  _ufo.Position = _ufoPos;

  // 指定位置に移動➁
  _ufo.Position += new Vector2(1, 0);

  // 指定した値だけ移動
  _ufo.Translate(new Vector2(1, 0));
  ```

実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年03月03日  
更新日：2022年03月05日 C#版を追加  
[[TOP]](#TOP)


<a id="マウス座標"></a>
# <b>マウス座標</b>

### 【GDScript版】 

 * 3D（Spatialノード）版  
  👇マウスの位置
    ```gdscript
    #Main.gd
    extends Spatial #2Dの場合はNode2D

    func _input(_event): # 入力イベント
      if _event is InputEventMouseMotion: # マウスを動かしている時
        print(_event.position) #-> (48, 425)
        print(_event.position.x) #-> 48
        print(_event.position.y) #-> 425
    ```
    👇入力座標位置  
    ```gdscript
    #Main.gd
    extends Spatial #2Dの場合はNode2D

    func _input(_event): # 入力イベント
      if _event is InputEventMouseButton: # マウスボタンを押した時
        if _event.button_index == 1: # マウスの左ボタン
          if _event.pressed: # 押している
            print(_event.position) #-> (48, 425)
            print(_event.position.x) #-> 48
            print(_event.position.y) #-> 425
    ```

 * 2D（Node2Dノード）版  
  👇マウスの位置
    ```gdscript
    # Main.gd
    extends Node2D

    var _ufo

    func _ready(): # 最初に一度だけ実行される
      _ufo = get_node("UFO")
      
    func _input(_event): # 入力イベント
      if _event is InputEventMouseMotion: # マウスを動かしている時
        _ufo.position.x = get_viewport().get_mouse_position().x
        _ufo.position.y = get_viewport().get_mouse_position().y
    ```
    👇入力座標位置  
    ```gdscript
    # Main.gd
    extends Node2D
      
    func _input(_event): # 入力イベント
      if _event is InputEventMouseButton: # マウスボタンを押した時
        if _event.button_index == 1: # マウスの左ボタン
          if _event.pressed: # 押している
            print(_event.position) #-> (216, 232)
            print(_event.position.x) #-> 216
            print(_event.position.y) #-> 232
    ```

### 【C#版】 

 * 3D（Spatialノード）版  
  👇マウスの位置
    ```c#
    // Main.cs
    using Godot;

    public class Main : Spatial {
      public override void _Input(InputEvent _event) {
        if (_event is InputEventMouseMotion _mouseEvent) {
          GD.Print(_mouseEvent.Position); //-> (423, 281)
          GD.Print(_mouseEvent.Position); //-> 423
          GD.Print(_mouseEvent.Position); //-> 281
        }
      }
    }
    ```
    👇入力座標位置  
    ```c#
    // Main.cs
    using Godot;

    public class Main : Spatial {
      public override void _Input(InputEvent _event) {
        if (_event is InputEventMouseButton _mouseEvent) {
          if (_mouseEvent.ButtonIndex == 1) {
            if (_mouseEvent.Pressed) {
              GD.Print(_mouseEvent.Position); //-> (282, 254)
              GD.Print(_mouseEvent.Position.x); //-> 282
              GD.Print(_mouseEvent.Position.y); //-> 254
            }	
          }
        }
      }
    }
    ```

 * 2D（Node2Dノード）版  
  👇マウスの位置
    ```c#
    // Main.cs
    using Godot;

    public class Main : Node2D {
      public override void _Input(InputEvent _event) {
        if (_event is InputEventMouseMotion _mouseEvent) {
          GD.Print(_mouseEvent.Position); //-> (337, 309)
          GD.Print(_mouseEvent.Position.x); //-> 337
          GD.Print(_mouseEvent.Position.y); //-> 309
        }
      }
    }
    ```
    👇入力座標位置  
    ```C#
    // Main.cs
    using Godot;

    public class Main : Node2D {
      public override void _Input(InputEvent _event) {
        if (_event is InputEventMouseButton _mouseEvent) {
          if (_mouseEvent.ButtonIndex == 1) {
            if (_mouseEvent.Pressed) {
              GD.Print(_mouseEvent.Position); //-> (357, 277)
              GD.Print(_mouseEvent.Position.x); //-> 357
              GD.Print(_mouseEvent.Position.y); //-> 277
            }
          }
        }
      }
    }
    ```

実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年03月06日  
[[TOP]](#TOP)


<a id="画面サイズ"></a>
# <b>画面サイズ</b>

 [プロジェクト]-[プロジェクト設定…]-[**Display**]-[**Window**]で以下の通りに設定  
  * Size
    * **Width** : 1920（初期値:1024）
    * **Height** : 1080（初期値:600）
    * Resizable : ✓オン（初期値）
    * **Fullscreen** : **✓**オン（初期値:オフ）
  * Dpi
    * **Allow Hidpi** : **✓**オン（初期値:オフ）
  * Handheld
    * Orientation : landscape（初期値）

実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年03月07日  
[[TOP]](#TOP)


<a id="背景色"></a>
# <b>背景色</b>

* [プロジェクト]-[プロジェクト設定…]-[**Rendering**]-[**Environment**]で以下の通りに設定
  * **Default Clear Color** : ffcc00（初期値:4d4d4d）

実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年03月07日  
[[TOP]](#TOP)


<a id="Rouletteゲーム"></a>
# <b>Rouletteゲーム</b>
[『Unityの教科書』](https://amzn.to/3hU5s5Z)のChapter3（オブジェクトの配置と動かし方）のGodot版  

### 【GDScript版】  
ルーレット画像（Sprite）に以下のスクリプトをアタッチ
```gdscript
# Roullette.gd
extends Sprite # 要注意！

var _rotSpeed = 0 # 回転速度
	
func _process(_delta): # 繰り返し実行
	# 回転速度ぶんルーレットを回転させる
	rotation += _rotSpeed
	_rotSpeed *= 0.98 # ルーレットを減速させる

# マウスが押されたら回転速度を設定する
func _input(_event): # 入力イベント
	if _event is InputEventMouseButton: # マウスを押したら
		if _event.button_index == 1: # マウスの左ボタン
			if _event.pressed: # 押している
				_rotSpeed = 3;
```

### 【C#版】  
```c#
// Roulette.cs
using Godot;

public class Roulette : Sprite { // 要注意！
    private float _rotSpeed = 0f; // 回転速度

    // 繰り返し実行される
    public override void _Process(float _delta) {
        // 回転速度ぶんルーレットを回転させる
        Rotation += _rotSpeed;
        _rotSpeed *= 0.98f; // ルーレットを減速させる
    }

    // マウスが押されたら回転速度を設定する
    public override void _Input(InputEvent _event) {
        if (_event is InputEventMouseButton _mouseEvent) {
            if (_mouseEvent.ButtonIndex == 1) { // 左ボタン
                if (_mouseEvent.Pressed) {
                    _rotSpeed = 3f;
                }
            }
        }
    }
}
```

参考ファイル：[Roulette.zip](https://github.com/mubirou/Godot/blob/main/zip/Roulette.zip)  
実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年03月10日  
[[TOP]](#TOP)


<a id="SwipeCarゲーム"></a>
# <b>SwipeCarゲーム</b>
[『Unityの教科書』](https://amzn.to/3hU5s5Z)のChapter4（UIと監督オブジェクト）のGodot版  

### 【GDScript版】  
メインシーン（Main.tscn）に以下のスクリプトをアタッチ
```gdscript
# Main.gd
extends Node2D

var _car
var _flag

func _ready():
	_car = get_node("Car")
	_flag = get_node("Flag")

func _process(_delta):
	var _distance = _flag.position.x - _car.position.x
	if _distance > 0 :
		_distance = "%10.2f" % (round(_distance)/20) # 少数点2桁表示
		$Label.text = str(_distance) + " m to the GOAL"
	else:
		$Label.text = "GAME OVER"
```

車（Sprite）に以下のスクリプトをアタッチ
```gdscript
# Car.gd
extends Sprite

var _speed = 0
var _startX
	
func _process(_delta):
	translate(Vector2(_speed, 0))
	_speed *= 0.98

func _input(_event):
	if _event is InputEventMouseButton:
		if _event.button_index == 1:
			if _event.pressed: # MouseDown
				_startX = _event.position.x
			else: # MouseUp
				var _disX = _event.position.x - _startX
				_speed = _disX / 20
				$AudioStreamPlayer2D.play() # 効果音は.wav
```

### 【C#版】  
メインシーン（Main.tscn）に以下のスクリプトをアタッチ
```c#
// Main.cs
using Godot;

public class Main : Node2D {
    private Node2D _car;
    private Node2D _flag;
    private Label _label;

    public override void _Ready() {
        _car = GetNode("Car") as Node2D;
        _flag = GetNode("Flag") as Node2D;
        _label = GetNode<Label>("Label");
    }

    public override void _Process(float _delta) {
        float _distance = _flag.Position.x - _car.Position.x;
        if (_distance > 0) {
            string _distanceText = (_distance/20).ToString("F2");
            _label.Text = _distanceText + " m to the GOAL";
        } else {
            _label.Text = "GAME OVER";
        }
    }
}
```

車（Sprite）に以下のスクリプトをアタッチ
```c#
// Car.cs
using Godot;

public class Car : Sprite {
    private float _speed = 0f;
    private float _startX;
    private AudioStreamPlayer2D _se;

    public override void _Ready() {
        _se = GetNode<AudioStreamPlayer2D>("AudioStreamPlayer2D");
    }

    public override void _Process(float _delta) {
        Translate(new Vector2(_speed, 0));
        _speed *= 0.98f;
    }

    public override void _Input(InputEvent _event) {
        if (_event is InputEventMouseButton _mouseEvent) {
            if (_mouseEvent.ButtonIndex == 1) {
                if (_mouseEvent.Pressed) { // MouseDown
                    _startX = _mouseEvent.Position.x;
                } else { // MouseUp
                    float _disX = _mouseEvent.Position.x - _startX;
                    _speed = _disX / 20;
                    _se.Play(); // SEは.wav
                }
            }
        }
    }
}
```


参考：[小数点以下2桁表示](https://docs.godotengine.org/ja/stable/tutorials/scripting/gdscript/gdscript_format_string.html#padding)、[外部フォント](https://note.com/doromaito/n/n60e16bdaa1be)、[効果音](http://blawat2015.no-ip.com/~mieki256/diary/202010211.html)  
参考ファイル：[SwipeCar.zip](https://github.com/mubirou/Godot/blob/main/zip/SwipeCar.zip)  
実行環境：Windows 10、Godot 3.4.2  
作成者：夢寐郎  
作成日：2022年03月23日  
更新日：2022年03月24日 C#版追加  
[[TOP]](#TOP)


<a id="220501"></a>
# <b>Quest + Oculus Link</b>

1. [Godot Standard version 64-bit(x86_64)](https://godotengine.org/download/windows) をダウンロード
1. [新規プロジェクト]（レンダラー：**OpenGL ES 2.0**）を作成
1. 最上段にある [AssetLib] から "**OpenXR Plugin**"（v.1.2.0）を [ダウンロード] ＆ [インストール]
1. [3Dシーン] を作成
1. [シーン]-[シーンを保存]
1. [ファイルシステム]-[res://]-[addons]-[godot-openxr]-[scenes]-[**first_person_controller_vr.tscn**] を上記の [シーン]-[Spatial] 上にドラッグ＆ドロップ  
1. [プロジェクト]-[プロジェクト設定]-[一般]-[Display]-[Window]-[**Use Vsync**] の ✓オン を外す（フレームレートを向上させるため）
1. [プリミティブ](#プリミティブ) など何かオブジェクトを配置（任意）し以下のような階層にする    
  Spatial  
　  ├ FPController（VR用カメラなど）  
　  └ MeshInstance（任意のオブジェクト）  
1. [**Oclus Linkの準備**](https://github.com/mubirou/Unity3D/tree/master/study-notes#oculus-link%E3%81%AE%E6%BA%96%E5%82%99) をする
1. Godot の [▶] を押して Quest + Godot が同時再生されれば成功！

参考：[framesynthesis.jp](https://framesynthesis.jp/tech/godot/vr/)  
実行環境：Windows 10、Godot 3.4.4 Standard  
Meta Quest（初代）v.39.0、Oculusアプリ v.39.0  
作成者：夢寐郎  
作成日：2022年05月01日  
[[TOP]](#TOP)


<a id="220502"></a>
# <b>Questコントローラー表示</b>

1. [Quest + Oculus Link](#220501) の設定をおこなう
1. 最上段にある [AssetLib] から "**Oculus Quest VR Toolkit**"（v.0.4.2）を [ダウンロード] ＆ [インストール]
1. [シーン]-[Main]-[**FPController**] を選択し右クリックし [編集可能な子] を [✓]
1. 同様に [ローカルにする] を選択
1. [ファイルシステム]-[res://]-[OQ_Toolkit]-[OQ_ARVRController]-[Models3d]-[**OculusQuestTouchController_Left.glft**] を上記で開いた [FPController]-[LeftHandController] 上にドラッグ＆ドロップ
1. 同様に [**OculusQuestTouchController_Right.glft**] を [RightHandController] 上にドラッグ＆ドロップ  
  Spatial  
　  ├ FPController（**ARVROrigin**）  
　  │   ├　**ARVRCamera**  
　  │   ├　LeftHandController（**ARVRController**）  
　  │   │　　└ OculusQuestTouchController_Left（.glTF）  
　  │   └　RightHandController（**ARVRController**）  
　  │　　  └ OculusQuestTouchController_Right（.glTF）  
　  └ MeshInstance（任意のオブジェクト）  
1. [Main] シーンに戻ってから [▶] を押して Quest + Godot が同時再生されコントローラーが表示されれば成功！（ボタン類は動かない）

参考：[docs.godotengine.org](https://docs.godotengine.org/ja/stable/tutorials/vr/xr_primer.html#new-ar-vr-nodes)

＜参考：Unity Asset Store の利用＞  
1. [Questコントローラー表示](https://github.com/mubirou/Unity3D/tree/master/study-notes#quest%E3%82%B3%E3%83%B3%E3%83%88%E3%83%AD%E3%83%BC%E3%83%A9%E3%83%BC%E8%A1%A8%E7%A4%BA)で必要な作業をおこなう
1. Unity の [Assets]-[Oculus]-[VR]-[Meshes]-[OculusTouchForQuestAndRiftS]-[**OculusTouchForQuestAndRiftS_Left.fbx**] および [**OculusTouchForQuestAndRiftS_Right.fbx**] を Godot のプロジェクトフォルダ内にコピー

実行環境：Windows 10、Godot 3.4.4  
作成者：夢寐郎  
作成日：2022年05月23日  
[[TOP]](#TOP)


<a id="220503"></a>
# <b>is_button_pressed()</b>

1. [検証用コード](#220503_1)
1. [検証結果](#220503_2)
1. [実践編](#220503_3)
1. [応用編（Down/Hold/Up）](#220503_4)

<a id="220503_1"></a>

### 検証用コード
[Questコントローラー](#220502)の LeftHandController または RightHandController にアタッチ済の controller.gd の _process(delta) 関数内に追加

```gdscript
if is_button_pressed(0): print("0")
if is_button_pressed(1): print("1")
if is_button_pressed(2): print("2")
if is_button_pressed(3): print("3")
if is_button_pressed(4): print("4")
if is_button_pressed(5): print("5")
if is_button_pressed(6): print("6")
if is_button_pressed(7): print("7")
if is_button_pressed(8): print("8")
if is_button_pressed(9): print("9")
if is_button_pressed(10): print("10")
if is_button_pressed(11): print("11")
if is_button_pressed(12): print("12")
if is_button_pressed(13): print("13")
if is_button_pressed(14): print("14")
if is_button_pressed(15): print("15")
if is_button_pressed(16): print("16")
if is_button_pressed(17): print("17")
if is_button_pressed(18): print("18")
if is_button_pressed(19): print("19")
if is_button_pressed(20): print("20")
if is_button_pressed(21): print("21")
if is_button_pressed(22): print("22")
if is_button_pressed(23): print("23")
if is_button_pressed(24): print("24")
if is_button_pressed(25): print("25")
if is_button_pressed(26): print("26")
if is_button_pressed(27): print("27")
if is_button_pressed(28): print("28")
if is_button_pressed(29): print("29")
if is_button_pressed(30): print("30")  
if is_button_pressed(31): print("31")
if is_button_pressed(32): print("32")
if is_button_pressed(64): print("64")
if is_button_pressed(71): print("71")
if is_button_pressed(128): print("128")
if is_button_pressed(256): print("256")
if is_button_pressed(512): print("512")
if is_button_pressed(1024): print("1024")
if is_button_pressed(2048): print("2048")
if is_button_pressed(4096): print("4096")
if is_button_pressed(8192): print("8192")
if is_button_pressed(16777216): print("16777216")
```
参考：[GODOT DOCS](https://docs.godotengine.org/ja/stable/classes/class_@globalscope.html#globalscope)  
["is_button_pressed()" TOP](#220503)  

<a id="220503_2"></a>

### 検証結果  
  [Questコントローラー](#220502)の LeftHandController または RightHandController にアタッチ済の controller.gd の _process(delta) 関数内に追加
  ```gdscript
  if is_button_pressed(1):
    if get_controller_id() == 1: print("Yを押した")
    if get_controller_id() == 2: print("Bを押した")

  if is_button_pressed(2):
    if get_controller_id() == 1: print("左中指トリガーを押した_50％")
    if get_controller_id() == 2: print("右中指トリガーを押した_50％")
    
  if is_button_pressed(3):
    print("MENUを押した")
    
  if is_button_pressed(5):
    if get_controller_id() == 1: print("Xにタッチ")
    if get_controller_id() == 2: print("Aにタッチ")

  if is_button_pressed(6):
    if get_controller_id() == 1: print("Yにタッチ")
    if get_controller_id() == 2: print("Bにタッチ")
    
  if is_button_pressed(7):
    if get_controller_id() == 1: print("Xを押した")
    if get_controller_id() == 2: print("Aを押した")
  
  if is_button_pressed(12):
    if get_controller_id() == 1: print("左アナログスティックにタッチ")
    if get_controller_id() == 2: print("右アナログスティックにタッチ")
    
  if is_button_pressed(14):
    if get_controller_id() == 1: print("左アナログスティックを押し込んだ")
    if get_controller_id() == 2: print("右アナログスティックを押し込んだ")
    
  if is_button_pressed(15):
    if get_controller_id() == 1: print("左人差し指トリガーを押した_70％")
    if get_controller_id() == 2: print("右人差し指トリガーを押した_70％")
  
  if is_button_pressed(16):
    if get_controller_id() == 1: print("左人差し指トリガーにタッチ_10％")
    if get_controller_id() == 2: print("右人差し指トリガーにタッチ_10％")
  ```
  参考：[GODOT DOCS](https://docs.godotengine.org/ja/stable/classes/class_@globalscope.html#globalscope)  
  ["is_button_pressed()" TOP](#220503)  

<a id="220503_3"></a>

### 実践編  
1. [Questコントローラー表示](#220502)の設定を行う
2. LeftHandController または RightHandController にアタッチ済の controller.gd を以下の通り変更
```gdscript
# controller.gd
extends ARVRController

signal activated
signal deactivated

signal LTriggerDown
signal RTriggerDown

func _process(delta):
  if get_is_active():
    if !visible:
      visible = true
      print("Activated " + name)
      emit_signal("activated")
  elif visible:
    visible = false
    print("Deactivated " + name)
    emit_signal("deactivated")
    
  if is_button_pressed(JOY_VR_TRIGGER): # 15
    if get_controller_id() == 1:
      emit_signal("LTriggerDown")
    if get_controller_id() == 2:
      emit_signal("RTriggerDown")
```
3. 大元の Spatial ノードの名前を Main に変更しスクリプト（Main.gd）をアタッチし以下の通りに記述  
```gdscript
# Main.gd
extends Spatial

var _LController
var _RController

func _ready():
  _LController = get_node("/root/Main/FPController/LeftHandController")
  _RController = get_node("/root/Main/FPController/RightHandController")
  # $"/root/Main/FPController/〇〇HandController" でも可
  
  _LController.connect("LTriggerDown", self, "LTriggerDownHandler")
  _RController.connect("RTriggerDown", self, "RTriggerDownHandler")

func LTriggerDownHandler():
  print("LTriggerDown")

func RTriggerDownHandler():
  print("RTriggerDown")
```
["is_button_pressed()" TOP](#220503)  


<a id="220503_4"></a>

### 応用編（Down/Hold/Up）

[Questコントローラー](#220502)の LeftHandController または RightHandController にアタッチ済の controller.gd の _process(delta) 関数内に追加

```gdscript
if is_button_pressed(JOY_VR_TRIGGER): # 15
	if get_controller_id() == 1:
		if !_isLTriggerDown:
			print("左人差し指トリガーを押した")
			_isLTriggerDown = true
		else: print("左人差し指トリガーを押し続けている") # 省略すると（downのみ）	
	if get_controller_id() == 2:
		if !_isRTriggerDown:
			print("右人差し指トリガーを押した")
			_isRTriggerDown = true
		else: print("右人差し指トリガーを押し続けている") # 省略すると（downのみ）
else:
	if _isLTriggerDown:
		_isLTriggerDown = false
		print("左人差し指トリガーを離した")
	if _isRTriggerDown:
		_isRTriggerDown = false
		print("右人差し指トリガーを離した")
```

実行環境：Windows 10、Godot 3.4.4  
作成者：夢寐郎  
作成日：2022年05月23日  
["is_button_pressed()" TOP](#220503)  
[[TOP]](#TOP)


<a id="220504"></a>
# <b>追跡</b>

Unity版の「[001 追跡](https://github.com/mubirou/Unity3D/blob/master/oqtouch/sample/README.md#001-%E8%BF%BD%E8%B7%A1)」のGodot版  

1. RightHandControl

```gdscript
# controller.gd
extends ARVRController

signal activated
signal deactivated
signal LTriggerDown
signal RTriggerDown
signal RTriggerHold
signal RTriggerUp

var _isLTriggerDown = false
var _isRTriggerDown = false

func _process(delta):
	if get_is_active():
		if !visible:
			visible = true
			print("Activated " + name)
			emit_signal("activated")
	elif visible:
		visible = false
		print("Deactivated " + name)
		emit_signal("deactivated")
	
	# Trigger
	if is_button_pressed(JOY_VR_TRIGGER): # 15
		if get_controller_id() == 1:
			if !_isLTriggerDown:
				print("左人差し指トリガーを押した")
				_isLTriggerDown = true
			#else: print("左人差し指トリガーを押し続けている") # 省略すると（downのみ）	
		if get_controller_id() == 2:
			if !_isRTriggerDown:
				emit_signal("RTriggerDown")
				#print("右人差し指トリガーを押した")
				_isRTriggerDown = true
			else:
				emit_signal("RTriggerHold")
				#print("右人差し指トリガーを押し続けている") # 省略すると（downのみ）
	else:
		if _isLTriggerDown:
			_isLTriggerDown = false
			print("左人差し指トリガーを離した")
		if _isRTriggerDown:
			_isRTriggerDown = false
			emit_signal("RTriggerUp")
			#print("右人差し指トリガーを離した")
```

1. Main

```gdscript
extends Spatial

var _rightHand
var _isRTriggerHold = false
var _piece0
var _pieceArray = []
var _pieceNum = 50

func _ready():
	_rightHand = get_node("/root/Main/FPController/RightHandController")
	_rightHand.connect("RTriggerDown", self, "RTriggerDownHandler")
	_rightHand.connect("RTriggerUp", self, "RTriggerUpHandler")
	_piece0 = get_node("piece")
	_pieceArray.append(_piece0)
	for i in range(1, _pieceNum):
		var _thePiece = _piece0.duplicate()
		add_child(_thePiece)
		_pieceArray.append(_thePiece)
	_piece0.hide()

func _process(delta):
	if !_isRTriggerHold: return
	_piece0.translation = _rightHand.translation
	for i in range(0, _pieceNum):
		var _thePiece  = _pieceArray[i]
		var _frontPiece = _pieceArray[i-1]
		var _disX = _frontPiece.translation.x - _thePiece.translation.x
		var _disY = _frontPiece.translation.y - _thePiece.translation.y
		var _disZ = _frontPiece.translation.z - _thePiece.translation.z
		_thePiece.look_at(_frontPiece.translation, Vector3.UP)
		var _thePos = _thePiece.translation
		_thePos.x += _disX / 8
		_thePos.y += _disY / 8
		_thePos.z += _disZ / 8
		_thePiece.translation = _thePos

func RTriggerDownHandler():
	_isRTriggerHold = true
	
func RTriggerUpHandler():
	_isRTriggerHold = false
```

実行環境：Windows 10、Godot 3.4.4  
作成者：夢寐郎  
作成日：2022年05月24日  
[[TOP]](#TOP)


<a id="220505"></a>
# <b>Questビルド</b>

自作 .apk ファイルを [SideQuest](https://sidequestvr.com/) を使って Meta Quest にインストールする方法  

📖 [SideQuest](https://sidequestvr.com/) とは…  
Meta の公式ストア以外のアプリを Meta Quest にインストール･削除等の操作を簡単に行える Windows 用ツール  

1. [Androidビルド](#Androidビルド)および、[FRAME SYNTHESIS](https://framesynthesis.jp/tech/godot/vr/)の「PC･Questで動作するVRアプリを作るには」を参考に **.apk** ファイルを作成する（特に以下の点に注意）  
    * [プロジェクト]-[プロジェクト設定]-[一般]-[Display]-[Window]-[Vsync]-[**Use Vsync**] の ✓ を外す  
    * [プロジェクト]-[プロジェクト設定]-[一般]-[Rendering]-[Vram Compression]-[**Import Etc**] を ✓ する
    * [プロジェクト]-[エクスポート]-[追加]-[Android]-[Xr Features]-[Xr Mode]-[**OpenXR**] に変更

1. [Quest を開発モードにする](https://github.com/mubirou/Unity3D/tree/master/metaquest#%E9%96%8B%E7%99%BA%E8%80%85%E3%83%A2%E3%83%BC%E3%83%89)

1. [SideQuestを使ってOculusQuestにapkファイルをインストールしよう！](https://vracademy.jp/blog/sidequest%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6oculusquest%E3%81%ABapk%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%82%88%E3%81%86/)の指示に従う（主な手順は以下の通り）  
    1. Windows に **SideQuest** をインストール
    1. Windows と **Quest** を接続
    1. SideQuest 上部の **Currently installed apps** アイコンを選択
    1. **Search package** の領域に上記で作成した **.apk** ファイルをドラッグ＆ドロップ
    1. **Quest** 上の [アプリ] の [**提供元不明**] の中からインストールしたアプリを選択し実行

参考：[VRアカデミー](https://vracademy.jp/blog/sidequest%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6oculusquest%E3%81%ABapk%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%82%88%E3%81%86/)、[FRAME SYNTHESIS](https://framesynthesis.jp/tech/godot/vr/)  
実行環境：Windows 10、Godot 3.4.4、SideQuest 0.10.27  
作成者：夢寐郎  
作成日：2022年05月26日  
[[TOP]](#TOP)


<a id="220506"></a>
# <b>オブジェクト色</b>

* オブジェクトの色付け  
  1. [シーン]-[＋]-[MeshInstance] で任意の[プリミティブ](#プリミティブ)を作成
  1. Mesh の [インスペクター]-[MeshInstance]-[**Material**]-[新規SpatialMaterial]-[編集]-[**Albedo**]-[Color] で #XXXXXX を指定

* 環境色を設定（初期設定はやや青系）  
  ※ オブジェクトの色は環境色に依存する  
  1. **res://default_env.tres** の [インスペクター]-[Background]-[Sky]-[Procedura]-[編集] を選択
  1. 次の通りに変更（例）  
      * **Top Color**：a5d6f1 → ffffff（太陽光）
      * **Horizon Color**：d6eafa → cccccc（地平線）

参考：[GODOT DOCS](https://docs.godotengine.org/ja/stable/tutorials/3d/environment_and_post_processing.html#environment-options)  
実行環境：Windows 10、Godot 3.4.4、Meta Quest（初代）v.40  
作成者：夢寐郎  
作成日：2022年05月28日  
[[TOP]](#TOP)


<a id="220507"></a>
# <b>床タイル</b>

📝床（10m四方）にタイル（1m四方）を貼る場合…

1. タイル（400x400px程度）のタイル（1m四方）用の画像を作成（例：[tile.svg](https://github.com/mubirou/Godot/blob/main/svg/tile.svg)）
1. [シーン]-[＋]-[MeshInstance] を選択
1. 名前を "MeshInstance" → "Floor" に変更
1. [インスペクター]-[MeshInstance]-[Mesh]-[新規**PlaneMesh**] を選択
1. 引続き [Spatial]-[Tranform]-[**Scale**] を次の通りに変更  
    * **x**：**10**、**z**：**10**（**10m**四方の床の場合）
1. 引続き [インスペクター]-[**Material**]-[[空]]-[新規**SpatialMaterial**] を選択
1. 表示された [球] に上記で作成した **.png** または **.jpg** をドラッグ＆ドロップ
1. [球] の右にある [v]-[編集]-[**Uv1**]-[**Scale**] を次の通りに変更  
    * **x**：**10**、**y**：**10**  

📝天井にタイルを貼る場合…  
※「PaneMesh」は裏は透明になる「CubeMesh」は裏は暗くなる、という問題を回避する必要があります
1. [シーン]-[＋]-[MeshInstance] を選択
1. 名前を "MeshInstance" → "Ceiling" に変更
1. [インスペクター]-[MeshInstance]-[Mesh]-[新規**CubeMesh**] を選択（2mの立方体）
1. [インスペクター]-[Transform] を次の通りに変更  
    * Transform：x 0、y 2.35、z 0
    * Scale：**x 5**、**y 0.01**、**z 5**
1. 引続き [インスペクター]-[**Material**]-[[空]]-[新規**SpatialMaterial**] を選択
1. 表示された [球] にタイル用の画像（**.png** または **.jpg**）をドラッグ＆ドロップ
1. [球] の右にある [v]-[編集] を選択し次の通りに変更
    * [**Flags**]-[**Unshaded**] を**✓**
    * [**Albedo**]-[**Color**] を設定（天井のベースカラー）
    * [**Uv1**] の設定は次の通り
        * [**Scale**]：**x** **5**、**z**：**5**
        * [**Triplanar Sharp**] を**✓**  

実行環境：Windows 10、Godot 3.4.4、Meta Quest（初代）v.40  
作成者：夢寐郎  
作成日：2022年05月28日  
更新日：2022年05月29日  
[[TOP]](#TOP)


<a id="220601"></a>
# <b>RayCastボタン</b>

💡 選択するオブジェクトの用意  
  1. [立方体](#プリミティブ)などを用意
  1. 上記を選択し [子ノードを追加]-[**KinematicBody**]
  1. KinematicBody を選択し [子ノードを追加]-[**CollisionShape**]
  1. CollisionShape を選択し [インスペクター]-[**Shape**]-[追加 BoxShape] を選ぶ（階層は以下の通り）  

　  ├ MeshInstance（選択するオブジェクト）  
　  │     └ **KinematicBody**（とにかく重要）  
　  │　　   └ **CollisionShape**（反応する領域）  

💡 RayCast の用意
  1. [[**FPController**](#220501)]-[**RightHandController**] にコントローラを視覚化させるオブジェクト（"ControllerR"）を用意
  1. RightHandController を選択し [子ノードを追加]-[**RayCast**]
  1. RayCast を選択し [インスペクター] の [**Cast To**] を [x 0、y 0、**z -1000**] に設定（階層は以下の通り）  

　  ├ FPController  
　  │   ├ Configuration  
　  │   ├ ARVRCamera  
　  │   ├ LeftHandController  
　  │   └ RightHandController  
　  │　　　　 ├ ControllerR（コントローラの視覚化）  
　  │　　　　 └ **RayCast**（最重要）  

💡 RayCast の視覚化
  1. RightHandController を選択し [子ノードを追加]-[**MeshInstance**] を選んで名前を "MeshInstance" → "RayLine" に変更
  1. RayLine を選択し [インスペクター]-[Mesh]-[新規 **CubeMesh**] を選ぶ
  1. 引続き [インスペクター]-[Transform] で次の通りに設定  
      * **Translation**：x 0、y 0、**z -1000**
      * **Scale**：x 0.003、y 0.003、**z 1000**
  1. 半透明にする  
      1. [インスペクタ]-[Material]-[新規 **SpatialMaterial**] を選択
      1. [編集] で以下の通りに設定  
          * [**Albedo**]-[**Color**]：**#80ffffff**（白･不透明度50％）
          * [**Flags**]-[**Transparent**]：**✓**

💡 ヒットしたポイントの視覚化
  1. RightHandController を選択し [子ノードを追加]-[**MeshInstance**] を選んで名前を "MeshInstance" → "HitPoint" に変更
  1. HitPoint を選択し [インスペクター]-[Mesh]-[新規 **SphereMesh**] を選ぶ
  1. 引続き [インスペクター]-[Transform] で次の通りに設定  
      * **Scale**：x 0.02、y 0.02、z 0.02  
  1. 半透明にする  
      1. [インスペクタ]-[Material]-[新規 **SpatialMaterial**] を選択
      1. [編集] で以下の通りに設定  
          * [**Albedo**]-[**Color**]：**#ccffffff**（白･不透明度80％）
          * [**Flags**]-[**Transparent**]：**✓**

（ここまでの作業の階層は以下の通り）  
  Spatial  
　  ├ FPController  
　  │   ├　Configuration  
　  │   ├　ARVRCamera  
　  │   ├　LeftHandController  
　  │   └　RightHandController  
　  │　　　　 ├ ControllerR（コントローラの視覚化）  
　  │　　　　 ├ **RayCast**（最重要）  
　  │　　　　 ├ RayLine（RayCastの視覚化）  
　  │　　　　 └ HitPoint（ヒットしたポイントの視覚化）  
　  └ MeshInstance（選択するオブジェクト）  
　　　　 └ **KinematicBody**（とにかく重要）  
　　　　　　　 └ **CollisionShape**（反応する領域）  

💡 コードの記述  

  * [RightHandController]-[controller.gd] に加筆  

  ```gdscript
  extends ARVRController

  signal activated
  signal deactivated
  signal TriggerDownR
  signal TriggerUpR

  var _isTriggerDownR = false

  func _process(delta):
    if get_is_active():
      if !visible:
        visible = true
        print("Activated " + name)
        emit_signal("activated")
    elif visible:
      visible = false
      print("Deactivated " + name)
      emit_signal("deactivated")

    if is_button_pressed(JOY_VR_TRIGGER): # 15
      if get_controller_id() == 2:
        if !_isTriggerDownR:
          _isTriggerDownR = true
          emit_signal("TriggerDownR")
    else:
      if _isTriggerDownR:
        _isTriggerDownR = false
        emit_signal("TriggerUpR")
  ```

実行環境：Windows 10、Godot 3.4.4 + OpenXR Plugin 1.2、Meta Quest 40.0  
作成者：夢寐郎  
作成日：202X年XX月XX日  
[[TOP]](#TOP)


<a id="XXX"></a>
# <b>平面に文字表示</b>

### これは編集中の項目です

1. [シーン]-[＋]-[Sprite3D]
1. [Sprite3D]-[＋子ノードを追加]-[Viewport]
1. [Sprite3D]-[インスペクター]-[Texture]-[[空]]-[v]-[新規ViewportTexture]-[（上記の）Viewport]
1. [Viewport]-[インスペクター]-[**Size**]-[x 512, y 512]
1. [Viewport]-[＋子ノードを追加]-[Panel]
1. [Panel]-[ブランチをシーンとして保存]→"Panel.tscn"
1. [Panel]-[インスペクター]-[Margin]-[**Right** 512, **Botton** 512]
1. [Panel] の領域に **〇〇.png** をドラッグ＆ドロップ
1. [Panel]-[インスペクター]-[Label]
1. [Label]-[インスペクター]-[Text]-"**〇〇〇〇**"
1. [Label]-[Theme Overrides]-[Fonts]-[[空]]-[v]-[新規DynamicFont]
1. [DynamicFont]-[編集]-[Settings]-[**Size**]-[32]
1. [DynamicFont]-[編集]-[Font]-[Font Data]-[[空]]-[v]-[新規DynamicFontData]
1. [DynamicFontData]-[**Font Path**]-"**KosugiMaru-Regular.ttf**"
1. [DynamicFontData]-[Settings]-[Use Mipmaps]-[✓] する？
1. [Sprite3D]-[インスペクター]-[**Flip V**]

実行環境：Windows 10、Godot 3.4.4、Meta Quest（初代）v.40  
作成者：夢寐郎  
作成日：202X年XX月XX日  
[[TOP]](#TOP)


<a id="XXX"></a>
# <b>XXXXX</b>

1. XXX
    ```c#
    XXXX
    ```
    * XXX
    * XXXX

実行環境：Windows 10、Godot 3.4.4  
作成者：夢寐郎  
作成日：202X年XX月XX日  
更新日：202X年XX月XX日  
[[TOP]](#TOP)


© 2021-2022 夢寐郎