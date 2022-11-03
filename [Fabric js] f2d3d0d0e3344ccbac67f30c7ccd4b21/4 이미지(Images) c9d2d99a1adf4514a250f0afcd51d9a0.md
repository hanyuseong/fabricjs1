
[목차로 이동](../%5BFabric%20js%5D%20f2d3d0d0e3344ccbac67f30c7ccd4b21.md)
# 4. 이미지(Images)

---

## 1. fabric.Image()

- fabric.Image 객체를 사용하여 특정 이미지 요소를 fabric에 전달

![Untitled](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled.png)
```javascript
<body>
    <canvas id="c"></canvas>
    <img src="/images/poster.jpg" id="img">
</body>

<script>
    let canvas = new fabric.Canvas('c');

		// 이미지 가져오기
    let imgEl = document.getElementById('img');
		// 이미지 속성 설정
    let imgInst = new fabric.Image(imgEl, {
        scaleX: .25,
        scaleY: .25,
        left: 70,
        top: 10,
        angle: 30
    });
    canvas.add(imgInst);
</script>
```

## 2. fabric.Image.fromURL(url,callbackopt)

- 문서에 이미지가 없고 이미지 URL만 있을 경우 사용
- URL을 통해 이미지가 확보되면 콜백 함수 실행

![Untitled](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%201.png)

```javascript
<body>
    <canvas id="c"></canvas>
</body>

<script>
    let canvas = new fabric.Canvas('c');

    fabric.Image.fromURL(
		'https://t1.daumcdn.net/cfile/tistory/2622DE4251F70C5B2A',
			 function(oImg) {
			      // 이미지 속성 설정
			      oImg.scale(0.25).set({flipX:true,angle:20,top:20,left:70}); 
			      canvas.add(oImg);
		     }
		);
</script>

```

## 3. fabric.Image.filters

- fabric은 기본적으로 몇 개의 필터를 제공하며, 직접 정의하는 것도 가능
- fabric.Image 인스턴스 내 필터 배열로 구성된 filters속성을 사용하여 적용

![▲ Grayscale](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%202.png)

▲ Grayscale

![▲ Contrast](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%203.png)

▲ Contrast

![                   ▲ Invert](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%204.png)

▲ Invert

![                ▲ Saturation](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%205.png)

▲ Saturation

![                    ▲ Sepia](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%206.png)

▲ Sepia

![                    ▲ Blur](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%207.png)

▲ Blur

![                   ▲ Noise](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%208.png)

▲ Noise

![                ▲ Vibrance](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%209.png)

▲ Vibrance

![                ▲ Brightness](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%2010.png)

▲ Brightness

![              ▲ HueRotation](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%2011.png)

▲ HueRotation

![                 ▲ Picelate](4%20%EC%9D%B4%EB%AF%B8%EC%A7%80(Images)%20c9d2d99a1adf4514a250f0afcd51d9a0/Untitled%2012.png)

▲ Picelate

```javascript
<body>
    <canvas id="c"></canvas>
</body>

<script>
    let canvas = new fabric.Canvas('c');

    // Grayscale
    fabric.Image.fromURL('/images/aladdin.jpg', function(img) {
        img.scale(0.35).set({left:55,top:20});

        // push() : 필터 추가
        img.filters.push(
            new fabric.Image.filters.Grayscale() // 흑백 효과
            new fabric.Image.filters.Sepia() // 세피아 효과
            new fabric.Image.filters.Brightness({ brightness: 0.7}) // 밝기: -1~1
            new fabric.Image.filters.Contrast({contrast: 0.25}) // 대비: -1~1
            new fabric.Image.filters.Blur({blur: 0.5}) // 블러: 0~1
            new fabric.Image.filters.HueRotation({rotation: -0.5}) // 색조: -1~1
            new fabric.Image.filters.Invert() // 반전
            new fabric.Image.filters.Noise({noise: 700}) // 노이즈
            new fabric.Image.filters.Pixelate({blocksize: 8}) // 픽셀화
            new fabric.Image.filters.Saturation({saturation: 1}) // 채도 : -1~1
            new fabric.Image.filters.Vibrance({vibrance: -0.5}) // 생동감 : -1~1
        ); 

        img.applyFilters(); // 필터 적용되면 캔버스를 다시 랜더링
        canvas.add(img); // 캔버스에 이미지 추가
    });
</script>
```