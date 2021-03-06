# Document

## create instance

#### `new MCanvas(width,height)` || `MCanvas(width,height)`:

create the canvas by width and height;

params:

	// the width of origin canvas;
	width : type : Number;
			 Default : 500;
			 required;

	// the height of origin canvas;
	height: type : Number;
			Default : width;
			optional;

## method

#### 1、 `mc.background(bg)`:

prepare background-image；

bg: optional ，default: init-bg；

> if you use `mc.background(bg)` before , then you can use `mc.background()` to reset to the init background.

params:

```js
bg : {
	// background-image,
	// type: url/HTMLImageElement/HTMLCanvasElement
    image:'' ,

    // type: origin / crop / contain
    	// origin : the width and height of canvas will be same as the image naturalWidth and naturalHeight, the init width and height will be invalid;
    	// crop : the image will covered with the canvas, can control crop by left and top;
    	// contain : the same as background-size:contain; can control postion by left and top;
    type:'origin',

    // the distance of leftTop corner of canvas;
    left:0,
    top:0,

    // the background-color of canvas;
    color:'#000000',
}
```

> TIPS：`background()` can use without `draw()`;

#### 2、`add(image,options)`/`add([{image:'',options:{}},{image:'',options:{}}])`:

prepare the source to draw on canvas;

params:

```js
// source，type: url/HTMLImageElement/HTMLCanvasElement
image : '',

options : {

	// example: width: 100 / '100%' / '100px';
    width:'100%',

    // crop params;
    crop:{
    	 // the distance to leftTop corner of source-image
        x:0,
        y:0,

        // example:100/'100%'/'100px'；
		 // the width and height will to be croped;
        width:'100%',
        height:'100%',
    },

    // position of source image;
    pos:{
    	 // example：
    	 // x: 250 / '250px' / '100%' / 'left:250' / 'center',
        x:0,
        y:0,

        // scale based on center point of source；
        scale:1,

        rotate:0,
    },
}

```
#### 3、`watermark(image,options)`:

prepare the watermark;

params:

```js
// type: url/HTMLImageElement/HTMLCanvasElement
image : '',

options:{
	// there must use percentage on canvas；
		// type : string
		// Default : '40%';
	width:'100%',

	// position
		// leftTop/leftBottom/rightTop/rightBottom;
		// type : string
		// Default : 'rightBottom';
	pos : 'leftTop',

	// the margin to border of canvas;
		// type : Number
		// Default : 20;
	margin :
}
```


#### 4、`text(context,options)`:

prepare the text;and you can use `<b>/<s>/<br>`;

params:

```js
// context，there provide 3 style of large/normal/small;
	// <b></b> : largeStyle  |  <s>小字</s> : smallStyle |  <br>
context : '<b>big</b>normal<br><s>small</s>',

options:{
	 // the width of text line;
	 // example :  width: 100 / '100%' / '100px';
    width : 300,

    // align of text line;
    // 'left'/'center'/'right';
    align : 'left',

    // the default normal font-size is 5% of the width of canvas;
    // smallStyle is 0.9 on normal;
    // largeStyle is 1.2 on normal;
    // default font-family is helvetica neue,hiragino sans gb,Microsoft YaHei,arial,tahoma,sans-serif;
    // default color is black;
    // lineheight is 1.1 on largeStyle;

	 // and you can set the style;
    // the style of contained in <s></s>
    smallStyle:{
        font : ``,
        color:'#000',
        lineheight: 100,
    },

    // the style of normal font
    normalStyle:{
        font : ``,
        color:'#000',
        lineheight: 100,
    },

    // the style of contained in <b></b>
    largeStyle:{
        font : '',
        color:'#000',
        lineheight: 100,
    },

    // the position of text on canvas;
    pos:{
    	 // example：
    	 // x: 250 / '250px' / '100%' / 'left:250' / 'center',
        x:0,
        y:0,
    },
};
```
#### 5、 `draw(fn)`:

final function ，`add`/`watermark`/`text` must use the `draw()` on the end, and it will export a base64 image that you can use in callback;

params:

```js
mc.draw({
    // the type of export image :  png/jpg/jpeg/webp;
    // default : png;
    type: 'png',

    //  the quality of export image : 0~1；
	//  it's invalid to png type;
    // default: .9;
    quality: 1,
    callback(b64){
        console.log(b64);
    }
})
```
