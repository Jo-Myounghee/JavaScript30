# 1. parseFloat()

> 문자열을 분석해 부동소수점 실수로 반환



```javascript
.map(parseFloat)
```

```javascript
.map(function(str) {
    return parseFloat
});
```

- 위의 두개는 동일

### 예시

```javascript
function circumference(r) {
  return parseFloat(r) * 2.0 * Math.PI;
}

console.log(circumference(4.567));
// expected output: 28.695307297889173

console.log(circumference('4.567abcdefgh'));
// expected output: 28.695307297889173

console.log(circumference('abcdefgh'));
// expected output: NaN
```



출처 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/parseFloat



# 2. Math.floor()

> 주어진 숫자와 같거나 작은 정수 중에서 가장 큰 수를 반환(== 내림)



```javascript
console.log(Math.floor(5.95)); //5
```



출처 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/floor

