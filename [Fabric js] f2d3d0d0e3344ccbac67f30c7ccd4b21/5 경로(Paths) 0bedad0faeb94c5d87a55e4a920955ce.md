
[목차로 이동](../%5BFabric%20js%5D%20f2d3d0d0e3344ccbac67f30c7ccd4b21.md)
# 5. 경로(Paths)

---

## 1. Paths란?

- 도형의 윤곽을 표시하고, 채우거나, 선을 그리고, 수정할 수 있는 기능
- 일련의 명령어들로 구성되며, 한 지점에서 다른 지점으로 펜으로 선을 긋는 듯한
명령어 구성이 가장 기본적인 형태

## 2. fabric.Path()

- M : 이동 / 펜을 해당 좌표로 이동
- L : 라인(선) 긋기 / 현재 위치에서 해당 좌표까지 선 긋기
- z : 닫기 / 그어지지 않은 각각의 path를 연결 짓는(닫는) 선을 강제로 그려줌
- C : 베지어 곡선 / 현재 위치에서 해당 좌표까지 곡선 그리기
- fabric 기본 객체와 마찬가지로 속성 설정 가능

![                            ▲ path 만들기](5%20%EA%B2%BD%EB%A1%9C(Paths)%200bedad0faeb94c5d87a55e4a920955ce/Untitled.png)!

                            ▲ path 만들기

![                             ▲ z가 없을 경우](5%20%EA%B2%BD%EB%A1%9C(Paths)%200bedad0faeb94c5d87a55e4a920955ce/Untitled%201.png)

                             ▲ z가 없을 경우

```javascript
<body>
    <canvas id="c"></canvas>
    <canvas id="d"></canvas>
</body>

<script>
    let canvas = new fabric.Canvas('c');
	  let canvas2 = new fabric.Canvas('d');

    // path 만들기
    let path = new fabric.Path('M 0 0 L 200 70 L 150 200 z');
    path.set({left: 70, top: 55, fill: 'green', stroke: 'red',
									strokeWidth: 5, opacity: 0.5}); // 속성 변경 가능
    canvas.add(path);

    // z가 없을 경우 -> 모양이 열려있음
    let path2 = new fabric.Path('M 0 0 L 20 130 L 50 20 L 20 70');
    path2.set({left: 70, top: 100, fill:'white', stroke: 'blue'});
    canvas2.add(path2);
</script>
```

## 3. fabric.loadSVGFromString() / fabric.loadSVGFromURL()

- 복잡한 path 구문은 수작업이 어려움

![Untitled](5%20%EA%B2%BD%EB%A1%9C(Paths)%200bedad0faeb94c5d87a55e4a920955ce/Untitled%202.png)

![Untitled](5%20%EA%B2%BD%EB%A1%9C(Paths)%200bedad0faeb94c5d87a55e4a920955ce/Untitled%203.png)

- 전체 SVG파일을 로드 → fabric의 SVG파서가 모든 SVG 요소들을 순환하여 그에 부합하는
Path 객체를 생성 → 그룹화(fabric.Group) → canvas에 추가/조작 가능

![Untitled](5%20%EA%B2%BD%EB%A1%9C(Paths)%200bedad0faeb94c5d87a55e4a920955ce/Untitled%204.png)

```javascript
<body>
    <button type="button" onclick="loadSVG();">svg</button>
    <canvas id="c"></canvas>
</body>

<script>
    let svgSrc = "http://fabricjs.com/assets/1.svg";
    let canvas = new fabric.Canvas('c');

    function loadSVG() {
        fabric.loadSVGFromURL(svgSrc, function (oSVG) {
            console.log(oSVG instanceof Array); // true -> 배열

            let obj = new fabric.Group(oSVG); // 배열 -> 하나의 객체로 그룹화
            obj.set({ left: 70, top: 150, angle: 20 });
            obj.scale(0.5);

            console.log(obj instanceof Array); // false
            console.log(obj instanceof Object); // true
            canvas.add(obj);
            canvas.renderAll();
        });
    }
</script>
```