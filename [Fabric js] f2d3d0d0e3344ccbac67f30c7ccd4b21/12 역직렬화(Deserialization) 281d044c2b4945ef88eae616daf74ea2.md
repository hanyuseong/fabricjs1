
[목차로 이동](../%5BFabric%20js%5D%20f2d3d0d0e3344ccbac67f30c7ccd4b21.md)
# 12. 역직렬화(Deserialization)

---

![Untitled](12%20%EC%97%AD%EC%A7%81%EB%A0%AC%ED%99%94(Deserialization)%20281d044c2b4945ef88eae616daf74ea2/Untitled.png)

## 1. loadfromJSON()

```javascript
<body>
    <canvas id="c"></canvas>
</body>

<script>
    var canvas = new fabric.Canvas('c');

    canvas.loadFromJSON('{"objects":[{"type":"rect","left":50,"top":50,"width":20,'+
                            '"height":20,"fill":"green","overlayFill":null,'+
                            '"stroke":null,"strokeWidth":1,"strokeDashArray":null,'+
                            '"scaleX":1,"scaleY":1,"angle":0,"flipX":false,'+
                            '"flipY":false,"opacity":1,"selectable":true,'+
                            '"hasControls":true,"hasBorders":true,'+
                            '"hasRotatingPoint":false,"transparentCorners":true,'+
                            '"perPixelTargetFind":false,"rx":0,"ry":0},'+
                            '{"type":"circle","left":100,"top":100,"width":100,'+
                            '"height":100,"fill":"red","overlayFill":null,'+
                            '"stroke":null,"strokeWidth":1,"strokeDashArray":null,'+
                            '"scaleX":1,"scaleY":1,"angle":0,"flipX":false,'+
                            '"flipY":false,"opacity":1,"selectable":true,'+
                            '"hasControls":true,"hasBorders":true,'+
                            '"hasRotatingPoint":false,"transparentCorners":true,'+
                            '"perPixelTargetFind":false,"radius":50}],'+
                            '"background":"rgba(0, 0, 0, 0)"}');
</script>
```

## 2. loadSVGFromString('...', function(objects, options){})

- 첫번째 인자(’...’)는 SVG문자열, 두번째 인자는 콜백함수

```javascript
<script>
    var canvas = new fabric.Canvas('c');

	fabric.loadSVGFromString('<?xml version="1.0" encoding="UTF-8" standalone="no" ?>'+
			                    '<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"'+
			                    ' "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">'+
			                    '<svg xmlns="http://www.w3.org/2000/svg" '+
			                    'xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"'+
			                    ' width="300" height="300" viewBox="0 0 300 300"'+
			                    ' xml:space="preserve"><desc>Created with Fabric.js '+
			                    '4.6.0</desc><defs></defs><rect x="0" y="0" width="100%"'+
			                    ' height="100%" fill="rgba(0, 0, 0, 0)"></rect>'+
			                    '<g transform="matrix(1 0 0 1 60.5 60.5)"  >'+
			                    '<rect style="stroke: none; stroke-width: 1; '+
			                    'stroke-dasharray: none; stroke-linecap: butt; '+
			                    'stroke-dashoffset: 0; stroke-linejoin: miter;'+
			                    ' stroke-miterlimit: 4; fill: rgb(0,128,0); '+
			                    'fill-rule: nonzero; opacity: 1;"  x="-10" y="-10" rx="0"'+
			                    ' ry="0" width="20" height="20" /></g>'+
			                    '<g transform="matrix(1 0 0 1 150.5 150.5)"  >'+
			                    '<circle style="stroke: none; stroke-width: 1; '+
			                    'stroke-dasharray: none; stroke-linecap: butt;'+
			                    ' stroke-dashoffset: 0; stroke-linejoin: miter;'+
			                    ' stroke-miterlimit: 4; fill: rgb(255,0,0); '+
			                    'fill-rule: nonzero; opacity: 1;"  cx="0" cy="0" r="50" />'+
			                    '</g></svg>',
			                    function(img) {

			                        console.log(img); // (3) [i, i, i] -> 배열상태 
			                        let obj = fabric.util.groupSVGElements(img); // 그룹화
			
			                        canvas.add(obj).renderAll();
			                    }
			                );
</script>
```