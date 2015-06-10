# WebFont_Haxe
Personal Guide to use the WebFontLoader with Haxe.\n
This how I use the [WebFontLoader](https://github.com/typekit/webfontloader) in my haxe project.

#Downloading WebFontLoader : 
The first step is to get the WebFontLoader code.
You can see the minified code [here](http://ajax.googleapis.com/ajax/libs/webfont/1.5.10/webfont.js).
You can then copy paste it into a file on your computer and then link it in your index.html file.
You can also get the webFontLoader file in this repo.
You should have something like that :
```HTML
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8"/>
		<meta name="viewport" content="initial-scale=1, user-scalable=no, minimal-ui">
		<title>My awesome game</title>
		
		<script type="text/javascript"  src="lib/webFontLoader.js"></script>
	</head>

	<body>
		<script src="pathToYourTranspiledJsFile.js"></script>
	</body>
</html>
```

#Font and CSS setup
You can use [font2web](http://www.font2web.com/) to convert your setup your font and CSS
In any case, once you have your font in your assets (I've put it in assets/fonts), you should have un CSS like this one : 
```CSS
@font-face {
	font-family: 'YourFont';
	src: url('assets/fonts/YourFont.ttf') format('truetype');
	font-weight: normal;
	font-style: normal;
}

```
Make sure that your .ttf link is first because Firefox (at least the version I used) wont load it if it's not the right format first

#Haxe Extern
The file you need is WebFontLoader.hx
The haxe extern that let you interact with the JS lib is almost empty.
As I know verry little about writting Haxe externs, this extern is far from being complete.
Once you've put this file in your project, you can start using the WebFontLoader with Haxe.
Here's an exemple how to :

```Haxe
import pathToTheFolderWichContainTheExtern.WebFontLoader;
class Main
{
	private var WebFontConfig:Dynamic;

	private function new(){
		WebFontConfig = {
		    custom: {
		    	families: ['YourFont'], // name of your fonts, same as the ones in the CSS
		    	urls: ['fonts.css'], // link to your CSS file(s)
		    },
		    
			/* active is the callback function called when all your fonts are ready */
			active: yourInitFunction
		};
		WebFontLoader.load(WebFontConfig);
	}
}
```

#Use with pixi.js
If like me you use pixi.js, here's how to use the loaded fonts :

```Haxe
import pixi.text.Text;
class Exemple {
	private function new(){
		var style:TextStyle = {font:"35px YourFont",align:"right"};
		var tempText = new Text("Test", style);
		addchild(tempText);
	}
}
```