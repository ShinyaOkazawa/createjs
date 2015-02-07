# createjsを始めてみる

## EaselJSとは
HTML5 Canvasでリッチな表現をするための近道

## やってみる

参考URL
[http://createjs.com/Docs/EaselJS/modules/EaselJS.html](http://createjs.com/Docs/EaselJS/modules/EaselJS.html)

canvas要素をラップするstageを作り、DisplayObjectインスタンスをstageの子として加える。

### EaselJSがサポートするDisplayObject
* Images - ```Bitmap```
* Vector画像 - ```Shape``` ```Graphics```
* アニメートされるビットマップ画像 - ```SpriteSheet``` ```Sprite```
* シンプルなテキストインスタンス - ```Text```
* 他のDisplayObjectを内包するコンテナ - ```Container```
* HTMLのDOM要素を操作する - ```DOMElement```

すべてのDisplayObjectはstageの子として加えられ、canvas内に描かれる。

*** ユーザーインタラクション ***

stageの中のすべてのdisplay object（DOMElementを除く）はmouseやtouchを使って操作が可能。EaselJSは、```hover```、```press```、```release```がサポートしていて、ドラッグ＆ドロップを使い易いようになっている。

*** シンプルな例 ***

EaselJSの描画APIを使用して、```Stage```上にどのように```Shape```を生成して配置しているかの例。

```javascript
// Create a stage by getting a reference to the canvas
stage = new createjs.Stage('demoCanvas');

// Create a Shape DisplayObject
circle = new createjs.Shape();
circle.graphics.beginFill('red').drawCircle(0,0,40);

// Set position of Shape instance
circle.x = circle.y = 50;

// Add Shape instance to stage display list
stage.addChild(circle);

// Update stage will render next frame
stage.update();
```
