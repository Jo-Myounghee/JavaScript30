# 1. fetch

> 필요할 때 서버에 네트워크 요청을 보내고 정보를 받아올 수 있는 방법 (AJAX, fetch 등등 다양함)

## 1) 기본 문법

```
let promise = fetch(url, [options])
```

- `url` - 접근하고자 하는 URL
- `options` - 선택 매개변수, method나 header 등을 지정할 수 있음
  - `options`에 아무것도 넘기지 않으면 요청은 `GET`메서드로 진행되어 `url`로부터 콘텐츠가 다운로드 됨



- `fetch()`를 호출하면 브라우저는 네트워크 요청을 보내고 promise가 반환됨

  -> 반환되는 promise는 `fetch()`를 호출하는 코드에서 사용됨



## 2) 응답 과정

1. 서버에서 응답 헤더를 받자마자 `fetch`호출 시 반환받은 `promise`가 내장 클래스 `Response`의 인스턴스와 함께 이행 상태가 됨

   - 아직 body가 도착하기 전이지만, 개발자는 응답 헤더를 보고 요청이 성공적으로 처리되었는지 아닌지 확인할 수 있음
   - 네트워크 문제나 존재하지 않는 사이트에 접속하려는 경우같이 HTTP 요청을 보낼 수 없는 상태에선 promise는 거부상태가 됨
   - HTTP 상태는 응답 프로퍼티를 사용해 확인할 수 있음
     - `status` - HTTP 상태 코드 (예: 200)
     - `ok` - boolean 값. HTTP 상태코드가 200대 인경우 `true`

   EX)

   ```
   let response = await fetch(url);
   
   if (response.ok) {// HTTP상태 코드가 200대인 경우
   	let json = await response.json();
   } else {
     alert("HTTP-Error: " + response.status);
   }
   ```

   

2. 추가 메서드를 호출해 응답 본문을 받음

   - `response`에는 promise를 기반으로 하는 다양한 메서드가 있음
     - `resonse.text()` - 응답을 읽고 텍스트를 반환
     - `response.json()` - 응답을 JSON 형태로 파싱
     - `response.formData()` - 응답을 `FormData` 객체 형태로 반환 ([FormData가 궁금하다면](https://ko.javascript.info/formdata))
     - `response.blob()` - 응답을 Blob(타입이 있는 바이너리 데이터)형태로 반환
     - `response.arrayBuffer()` - 응답을 ArrayBuffer(바이너리 데이터를 로우 레벨 형식으로 표현한 것)형태로 반환

출처 : https://ko.javascript.info/fetch

---

