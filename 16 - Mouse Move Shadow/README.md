# 1. 변수 할당

```javascript
const width = hero.offsetWidth;
const height = hero.offsetHeight;
```

> const { offsetWidth: width, offsetHeight: height } = hero;

```javascript
let x = e.offsetX;
let y = e.offsetY;
```

> let { offsetX: x, offsetY: y } = e;



# 2. Math.round

- 입력 값을 반올림한 수와 가장 가까운 정수 값 반환



출처 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/round



# 3. css변수

```html
<style>
    h1 {
        text-shadow: 10px 10px 0 rgba(0, 0, 0, 1);
    }
</style>

<script>
    const hero = document.querySelector('.hero');
	const text = hero.querySelector('h1');
    
    text.style.textShadow = `
		10px 10px 0 red,
		20px 20px 0 yello
	`;
</script>
```

> css 속성 이름이 `-`으로 되어있으면 script에서 선택할 때는 대문자로 씀

