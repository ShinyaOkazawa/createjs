# createjsを始めてみる

## EaselJS
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

**ユーザーインタラクション**

stageの中のすべてのdisplay object（DOMElementを除く）はmouseやtouchを使って操作が可能。EaselJSは、```hover```、```press```、```release```がサポートしていて、ドラッグ＆ドロップを使い易いようになっている。

**シンプルな例**

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

**シンプルなインタラクションの例**

```javascript

displayObject.addEventListener('click', handleClick);

function handleClick(event){
	// Click happenened
}

displayObject.addEventListener('mousedown', handlePress);

function handlePress(event){
	// A mouse press happened
	// Listen for mouse move while the mouse is down
	event.addEventListener('mousemove', handleMove);
}

function handleMove(event){
	// Check out the DragAndDrop example in GitHub for more
}

```

**シンプルなアニメーションの例**

```javascript
// Update stage will render next frame
createjs.Ticker.addEventListener('tick', handleTick);

function handleTick(){

	// Circle will move 10 units to the right
	circle.x += 10;

	// Will cause the circle to wrap back
	if(circle.x > stage.canvas.width){
		circle.x = 0;
	}

	stage.update();
}
```

**他の特徴**

EaselJSは下記をサポートしている。
* Canvasの特徴である```Shadow```や```CompositeOperation```
* ```Ticker```
* Filter類、```ColorMatrixFilter```、```AlphaMaskFilter```、```AlphaMapFilter```、```BlurFilter```などなど
* ```ButtonHelper```ユーティリティはインタラクティブなボタンを簡単に作ることができる
* ```SpriteSheetUtils```、```SpriteSheetBuilder```は```SpriteSheet```の機能性を実行時に組み立て、操作するのを補助する

**ブラウザサポート**

canvasをサポートするブラウザであれば、EaselJSはサポートされる。(IE9以上)

[canvasが利用可能なブラウザ](http://caniuse.com/#feat=canvas)

* * *

## TweenJS

TweenJSライブラリは、シンプルでパワフルなトゥイーンインタフェースを提供します。数値オブジェクトのプロパティと、CSSのプロパティをサポートします。トゥイーンとアクションを同時に行い、複雑な動きを作ることが可能です。

**シンプルなトゥイーン**

```javascript

	var stage = new createjs.Stage('demoCanvas');

	var circle = new createjs.Shape();
	circle.graphics.beginFill('DeepSkyBlue').drawCircle(0,0,50);
	circle.x = 100;
	circle.y = 100;
	stage.addChild(circle);

	createjs.Tween.get(circle, { loop: true })
		.to({ x: 400 }, 1000, createjs.Ease.getPowInOut(4))
		.to({ alpha: 0, y: 175}, 500, createjs.Ease.getPowInOut(2))
		.to({ alpha: 0, y: 225}, 100)
		.to({ alpha: 1, y: 200}, 500, createjs.Ease.getPowInOut(2))
		.to({ x: 100 }, 800, createjs.Ease.getPowInOut(2));

	createjs.Ticker.setFPS(60);
	createjs.Ticker.addEventListener('tick', stage);
	
```

# 01 画像をトゥイーンアニメーションさせる

## 画像ファイルの読み込み、canvas上に反映

createjsをCDNで読み込む。

```

<script src="https://code.createjs.com/createjs-2014.12.12.min.js"></script

```

body要素にcanvasを加える。

```

<canvas id="canvas" width="500" height="300"></canvas>

```

EaselJSはcanvas上にStageオブジェクトを作成する。

```

stage = new createjs.Stage(canvas);

```

PreloadJSを利用して、画像を読み込み、stage上に画像を表示させる。

```

var queue = new createjs.LoadQueue(false);

queue.on('complete', draw);
queue.loadManifest([
	{id: 'img', src: 'circle.png'}
]);

function draw(){
	var bitmap;
	var image = queue.getResult('img');

	bitmap = new createjs.Bitmap(image);

	stage.addChild(bitmap);
	stage.update();
}
			
```

**注意点**
ここでのdraw()関数は関数式で書くと動作しない。関数宣言で行う。
理由としては、関数式で書くと、「関数の巻き上げ」が起こらないため。

```queue.on('complete', draw)```の後にdraw関数があるため関数式ではエラーになる。


