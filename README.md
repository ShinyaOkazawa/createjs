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
