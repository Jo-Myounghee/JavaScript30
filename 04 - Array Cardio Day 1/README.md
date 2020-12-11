# 1. map()

## 1) 사용하는 방법

`배열.map((요소, 인덱스, 배열) => { return.요소 });`

- 반복문을 돌며 배열 안의 요소들을 1대 1로 짝지어줌



## 2) 예시

```javascript
const oneTwoThree = [1, 2, 3];
let result = oneTwoThree.map((v) => {
	console.log(v);
	return v;
});
// 콘솔에는 1, 2, 3이 찍힘
oneTwoThree; // [1, 2, 3]
result; // [1, 2, 3]
oneTwoThree === result; // false

result = oneTwoThree.map((v) => {
    return v + 1;
});
result; // [2, 3, 4]

result = oneTwoThree.map((v) => {
    if (v % 2) {
        return '홀수';
    }
    return '짝수';
});
result; // ['홀수', '짝수', '홀수']
```



# 2. reduce()

## 1) 사용법

`배열.reduce((누적값, 현잿값, 인덱스, 요소) => { return 결과 }, 초깃값);`

- 누적값

## 2) 예시

```javascript
const oneTwoThree = [1, 2, 3];
let result = oneTwoThree.reduce((acc, cur, i) => {
    console.log(acc, cur, i);
    return acc + cur;
}, 0);
// 0 1 0
// 1 2 1
// 3 3 2
result;  // 6
```

- acc(누적값)이 초깃값인 0부터 시작해서 return하는대로 누적됨
- 초깃값을 적어주지 않으면 자동으로 초깃값이 0번째 인덱스의 값이 됨 

```javascript
const oneTwoThree = [1, 2, 3];
let result = oneTwoThree.reduce((acc, cur, i) => {
    console.log(acc, cur, i);
    return acc + cur;
});
// 1 2 1
// 3 3 2
result; // 6
```



```javascript
const oneTwoThree = [1, 2, 3];
let result = oneTwoThree.reduce((acc, cur, i) => {
    acc.push(cur % 2 ? '홀수' : '짝수');
    return acc;
}, []);
result; // ['홀수', '짝수', '홀수']
```

- 초기값을 배열로 만들고 배열에 값들을 push하면 map과 같아짐

  이를 응용하여 조건부로 push를 하면 filter와 같아짐



```javascript
const oneTwoThree = [1, 2, 3];
let result = oneTwoThree.reduce((acc, cur, i) => {
    if (cur % 2) acc.push(cur);
    return acc;
}, []);
result; // [1, 3]
```

> 홀수만 필터링 하는 코드



```javascript
const promiseFactory = (time) => {
    return new Promise((resolve, reject) => {
        console.log(time);
        setTimeout(resolve, time);
    });
};
[1000, 2000, 3000, 4000].reduce((acc, cur) => {
    return acc.then(() => promiseFactory(cur));
}, Promise.resolve());
// 바로 1000
// 1초 후 2000
// 2초 후 3000
// 3초 후 4000
```

- 초깃값을 Promise.resolve()로 한 후에, return된 프로미스에 then을 붙여 다음 누적값으로 넘기면 됨

  프로미스가 순차적으로 실행됨을 보장할 수 있음



## 3) reduceRight

```javascript
const oneTwoThree = [1, 2, 3];
let result = oneTwoThree.reduce((acc, cur, i) => {
    console.log(acc, cur, i);
    return acc + cur;
}, 0);
// 0 3 2
// 3 2 1
// 5 1 0
result; // 6
```

- `reduce`와 동작은 같지만 요소 순회를 오른쪽에서부터 왼쪽으로 한다는 점이 다름

