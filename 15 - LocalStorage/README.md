# 1. preventDefault()

- `a`태그나 `submit`태그는 고유의 동작이 있다. (페이지를 이동시킨다거나 `form`안에 있는 `input` 등을 전송한다거나...)

  -> 이런 동작을 중단시키는 것 == `preventDefault()`

출처 : https://pa-pico.tistory.com/20

# 2. submit

>  addEventListener('`submit`', addItem);

- submit은 click, enter다 되기 때문에 `click`이벤트 대신 `submit`이벤트를 사용했다.



# 3. 추가하고 싶은 점

- delete 버튼