
[목차로 이동](../%5BFabric%20js%5D%20f2d3d0d0e3344ccbac67f30c7ccd4b21.md)
# 13. 서브클래싱(Subclassing)

## 1. fabric.util.createClass()

- fabric은 객체지향적인 방식으로 제작 → 계층 구조가 존재
- 모든 2D객체(paths, images, text, etc.)는 fabric.Object와 일부 클래스를 상속 받음
- 새로운 클래스 생성하기
    - initalize : 유일한 속성으로 생성자로 사용

```javascript
<script>
    let Point = fabric.util.createClass({
        initialize: function(x, y) {
            this.x = x || 0;
            this.y = y || 0;
        },
        toString: function() {
            return this.x + '/' + this.y;
        }
     });
</script>
```

- 자식 클래스 만들기
    - 첫번째 인자 : 부모클래스
    - callSuper() : 부모 클래스의 메서드를 호출

```javascript
<script>
	let ColoredPoint = fabric.util.createClass(Point, {
        initialize: function(x, y, color) {
            this.callSuper('initialize', x, y);
            this.color = color ||'#000';
        },
        toString: function() {
            return this.callSuper('toString') + ' (color: ' + this.color + ')';
        }
   });
</script>
```

## 2. fabric 기본 객체 활용하기

![Untitled](13%20%EC%84%9C%EB%B8%8C%ED%81%B4%EB%9E%98%EC%8B%B1(Subclassing)%2011c54d343dd840ddaa774ace9f491c22/Untitled.png)

```javascript
<body>
    <canvas id="c"></canvas>
</body>

<script>
    let canvas = new fabric.Canvas('c');

    // fabric.Rect 상속받아 새로운 클래스 정의하기
    let LabeledRect = fabric.util.createClass(fabric.Rect, {
  
        type: 'labeledRect', // type설정
        
        initialize: function(options) {
            options || (options = {});
            
            // callSuper를 활용하여 initialize 재정의
            this.callSuper('initialize', options);
            this.set('label', options.label || '');
        },
        
        // toObject로 객체 표현할 경우 label도 추가되야 하므로 확장해줘야함
        toObject: function() {
            return fabric.util.object.extend(this.callSuper('toObject'), {
                label: this.get('label')
            });
        },
        
        // _render : 인스턴스를 실제로 그리는 것
        _render: function(ctx) {
            this.callSuper('_render', ctx);
            
            ctx.font = '20px Helvetica';
            ctx.fillStyle = 'white';
            ctx.fillText(this.label, -this.width/3.5, this.height/5);
        }
    });

    // LabeledRect 생성
    let labeledRect = new LabeledRect({
        width: 100,
        height: 50,
        left: 100,
        top: 30,
        label: 'hello!',
        fill: 'blue'
    });

    let labeledRect2 = new LabeledRect({
        width: 250,
        height: 30,
        left: 30,
        top: 100,
        label: 'nice to meet you',
        fill: '#aaf',
        rx: 10,
        ry: 10
    });

    canvas.add(labeledRect,labeledRect2);
</script>
```