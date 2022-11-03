
[목차로 이동](../%5BFabric%20js%5D%20f2d3d0d0e3344ccbac67f30c7ccd4b21.md)
# 7. 색상 & 그라디언트(Colors & Gradients)

## 1. 색상(Colors)

- 다양한 방식으로 색상 지원  : hex(16진수), RGB, RGBA

```javascript
// 색상정의
new fabric.Color('#f55');
new fabric.Color('#123123');
new fabric.Color('356735');
new fabric.Color('rgb(100,0,100)');
new fabric.Color('rgba(10, 20, 30, 0.5)');
```

- 변환이 쉬움
    - toHex() : 색상 인스턴스를 16진수로 변환
    - toRgb() : 색상 인스턴스를 RGB1로 변환
    - toTgba() : 색상 인스턴스를 알파 채널이 있는 RGB로 변환

```javascript
new fabric.Color('#f55').toRgb();//"rgb(255,85,85)"
new fabric.Color('rgb(100,100,100)').toHex();//"646464"
new fabric.Color('fff').toHex();//"FFFFFF"
```

## 2. 그라디언트(Grandients)

- 한 색을 다른 색으로 혼합하여 그래픽 효과를 만들어 내는 표현 방법
- 그라디언트를 먼저 만든 후 객체에 채우기 또는 획으로 할당

![Untitled](7%20%EC%83%89%EC%83%81%20&%20%EA%B7%B8%EB%9D%BC%EB%94%94%EC%96%B8%ED%8A%B8(Colors%20&%20Gradients)%20960aa526dc034b319b4bac0f257e97a1/Untitled.png)
```javascript
<body>
    <canvas id="c"></canvas>
</body>

<script>
    let canvas = new fabric.Canvas('c');

    let circle = new fabric.Circle({
        left: 105,
        top: 45,
        radius: 40
    });

    let circle2 = new fabric.Circle({
        left: 105,
        top: 155,
        radius: 40,
        fill: 'red'
    });

    // linear
    let gradient1 = new fabric.Gradient({
        type: 'linear', // or radial
        gradientUnits: 'pixels', // or 'percentage'

        // 그라디언트가 확장되는 방식을 정의
				// 최소 2개의 좌표 쌍(x1,y1,x2,y2 ...) 필요
        coords: { x1: 0, y1: 0, x2: 0, y2: circle.height },

        // 색상(배열)
        colorStops:[
            { offset: 0, color: 'red' },
            { offset: 1, color: '#fff'}
        ]
    });
		// 생성한 그라디언트 객체에 적용
		circle.set('fill', gradient1);

    // radial
    let gradient2 = new fabric.Gradient({
        type: 'radial',
        coords: {
            r1: 50,
            r2: 2,
            x1: 35,
            y1: 35,
            x2: 35,
            y2: 35
        },
        colorStops:[
            { offset: 0, color: 'black' },
            { offset: 1, color: 'white'}
        ]
    })
    circle2.set('fill', gradient2);

    canvas.add(circle,circle2);
</script>
```