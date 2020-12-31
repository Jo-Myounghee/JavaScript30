# 1. 배운 점

## 1) Date.now()

- 1970년 1월 1일 0시 0분 0초부터 현재까지 경과된 밀리 초를 반환
- setInterval 함수와 함께 사용하면 일정 시점부터 경과시간 측정 가능

출처 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/now

## 2) setInterval(function, delay)

- 일정 시간마다 함수를 실행

- 예시

  ```javascript
  setInterval(function(){console.log('hi')}, 1000)
  // 1초마다 'hi'출력
  ```

- 주의사항

  ```javascript
  setInterval(console.log('hi'), 1000)
  // 'hi'가 한 번만 출력됨
  ```

  - 함수를 반복해서 실행하는 것이기 때문에 함수로 쓰지 않으면 반복 실행이 안됨

## 3) clearInterval()

- setInterval로 반복하고 있는 것을 멈추게 함

- 예시

  ```javascript
  let count = 0;
  let repeat = setInterval(function() {
      console.log('setInterval');
      count++;
      if(count===5) {
          clearInterval(repeat);
      }
  }, 1000)
  ```

출처 : https://squll1.tistory.com/entry/javascript-setTimeout-setInterval-clearInterval

# 2. 추가하고 싶은 점

- [ ] 0:00이 되면 timeover 글자 나오게 추가