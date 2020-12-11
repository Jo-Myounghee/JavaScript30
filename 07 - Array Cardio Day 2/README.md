# 1. 전개 구문

> 배열이나 문자열과 같이 반복 가능한 문자를 
>
> 0개 이상의 인수 (함수로 호출할 경우) 또는 요소 (배열 리터럴의 경우)로 확장하여,
>
> 0개 이상의 키-값의 쌍인 객체로 확장 시킬 수 있음

## 1) 함수 호출

```javascript
myFunction(...iterableObj);
```

## 2) 배열 리터럴과 문자열

```javascript
[...iterableObj, '4', 'five', 6];
```

## 3) 객체 리터럴(ECMAScript 2018에서 추가)

```javascript
let objClone = { ...obj };
```

## 4) 예제

### (1) 함수 호출에서의 전개

#### 1. `apply()`대체

> 일반적으로 배열의 엘리먼트를 함수의 인수로 사용하고 싶을 때 `Function.prototype.apply()`사용
>
> -> 전개구문으로 대체 가능

##### 기존 코드

```javascript
function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction.apply(null, args);
```

##### 바꾼 코드

```javascript
function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction(...args);
```

#### 2. 인수 목록의 모든 인수는 전개 구문 사용 가능 & 여러번 사용 가능

```javascript
function myfunction(v, w, x, y, z) { }
var args = [0, 1];
myFunction(-1, ...args, 2, ...[3]);
```

#### 2. `new`에 적용

> `new`를 사용해 생성자를 호출할 때, 배열과 `apply`를 직접사용하는 것이 불가했음.
>
> but, 전개 구문을 사용해서 쉽게 사용 가능

```javascript
var dateFields = [1970, 0, 1];
var d = new Date(...dateFields);
```

- 전개 구문 없이 파라미터의 배열과 함께 `new`를 사용하려면, 부분적인 어플리케이션을 통해 **간접적**으로 해야함



### (2) 배열 리터럴에서의 전개

```javascript
var parts = ['shoulders', 'knees'];
var lyrics = ['head', ...parts, 'and', 'toes'];
// ['head', 'shoulders', 'knees', 'and', 'toes']
```

#### 1. 배열 복사

```javascript
var arr = [1, 2, 3];
var arr2 = [...arr]; // arr.slice()와 유사
arr2.push(4);

// arr2는 [1, 2, 3, 4]이 됨
// arr은 영향을 받지 않고 남아 있음
```

```javascript
var a = [[1], [2], [3]];
var b = [...a];
b.shift().shift(); // 1
// 이제 배열 a도 영향을 받음: [[], [2], [3]]
```

#### 2. 배열을 연결하는 더 나은 방법

##### 1) `Array.prototype.concat()`

> 배열을 존재하는 배열의 끝에 이어붙이는데 사용

##### 전개 구문을 사용하지 않는 경우

##### 전개 구문 없이 작성하는 방법

```javascript
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
// arr2의 모든 항목을 arr1에 붙임
arr1 = arr1.concat(arr2);
```

##### 전개 구문을 사용하는 경우

```javascript
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1 = [...arr1, ...arr2]; // arr1은 이제 [0, 1, 2, 3, 4, 5]
```

##### 2) `Array.prototype.unshift()`

> 존재하는 배열의 시작 지점에 배열의 값들을 삽입하는데 사용

##### 전개 구문을 사용하지 않는 경우

```javascript
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
// arr2의 모든 항목을 arr1의 앞에 붙임
Arrary.prototype.unshift.apply(arr1, arr2) // arr1은 이제 [3, 4, 5, 0, 1, 2]가 됨
```

##### 전개 구문을 사용하는 경우

```javascript
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1 = [...arr2, ...arr1]; // arr1은 이제 [3, 4, 5, 0, 1, 2]가 됨
```



출처 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax

