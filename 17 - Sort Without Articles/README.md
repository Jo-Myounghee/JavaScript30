[toc]



# 1. 정규표현식(==정규식)

> - 정규 표현식은 문자열에 나타나는 특정 문자 조합과 대응시키기 위해 사용되는 패턴
>
> - 자바스크립트에서 정규 표현식 또한 객체임
> - 이 패턴들은 `RegExp`의 `exec`메소드, `test`메소드, `String`의 `match`메소드, `replace`메소드, `search`메소드, `split`메소드와 함께 쓰임



### 1) 정규표현식 만들기

#### (1) 정규식 리터럴(슬래쉬'`/`'로 감싸는 패턴)

```javascript
var re = /ab+c/;
```

- 정규식 리터럴은 스크립트가 불러와질 때 컴파일 됨.
- **정규식이 상수라면** 슬래쉬로 감싸는 패턴을 사용하는 것이 성능을 향상시킬 수 있음



#### (2) `RegExp`객체의 생성자 함수를 호출하는 방법

```javascript
var re = new RegExp('ab+c');
```

- 생성자 함수를 사용하면 정규식이 실행 시점에 컴파일 됨
- **정규식의 패턴이 변경될 수 있는 경우, 사용자 입력과 같이 다른 출처로부터 패턴을 가져와야하는 경우**에 생성자 함수 사용



### 2) 정규식 패턴 작성하기

> 정규식 패턴은 `/abc`와 같이 단순 문자로 구성될 수도 있고, `/ab*c/`또는 `/Chapter(\d+)\.\d*/`와 같이 단순 문자와 특수 문자의 조합으로 구성될 수도 있음.



#### (1) 단순 패턴 사용하기

> 문자열을 있는 그대로 대응시키고자 할 때 사용

- `/abc`라는 패턴은 문자열에서 정확히 'abc'라는 문자들이 모두 함께 순서대로 나타나야 대응됨
- 위의 패턴은 "Hi, do you know your abc's?" 혹은 "The slabcraft"에서 부분 문자열 'abc'에 대응될 것
- 'Grab crab'이라는 문자열에서 'ab c'라는 부분 문자열을 포함하고 있지만 'abc'를 정확하게 포함하고 있지 않기 때문에 대응되지 않음

#### (2) 특수 문자 사용하기

> 검색에서 하나 이상의 b들을 찾거나, 혹은 공백을 찾는 것과 같이 '있는 그대로의 대응' 이상의 대응을 필요로 할 경우, 패턴에 특수한 문자를 포함시킴

- `/ab*c/`패턴은  'a'문자 뒤에 0개 이상의 'b'문자(`*`문자는 바로 앞의 문자가 0개 이상이라는 것을 의미함)가 나타나고 바로 뒤에 'c'문자가 나타나는 문자 조합에 대응됨.
- 문자열 "cbbabbbbcdebc"에서 위의 패턴은 부분 문자열 'abbbbc'와 대응됨



##### <정규식에서의 특수문자>

- `\`
  - 특수 문자가 아닌 문자(non-special character) 앞에서 사용된 백슬래시
    - 해당 문자는 특별하고, 문자 그대로 해석되면 안됨
      - ex
        - `b` == 'b'
        - `\b` != 'b'  ---> 특수문자로서 "단어 경계"에 대응됨
  - 특수 문자 앞에 위치한 백슬래시
    - 다음에 나오는 문자는 특별하지 않고, 문자 그대로 해석되어야한다.
    - ex
      - `/a*/` --> 특수문자 '`*`'은 0개 이상의 'a'문자가 등장함을 나타냄
      - `/a\*/` == `'a*'`--> '`*`'이 특별하지 않다는 것을 나타냄 

- `^`

  - 입력의 시작 부분에 대응됨
  - 만약 다중행 플래그가 참으로 설정되어 있다면 줄 바꿈 문자 바로 다음 부분과도 대응됨
  - ex
    - `/^A/` 는 "an A"의 A와는 대응되지 않지만, "An E"의 "A"와는 대응됨

- `$`

  - 입력의 끝 부분과 대응됨
  - 만약 다중행 플래그가 참으로 설정되어 있다면, 줄 바꿈 문자의 바로 앞 부분과도 대응됨

  - ex
    - `/t$/`는 "eater"의 't'에는 대응되지 않지만, "eat"과는 대응됨

- `*`

  - 앞의 표현식이 0회 이상 연속으로 반복되는 부분과 대응됨
  - `{0,}`와 같은 의미
  - ex
    - `/bo*/`는 "A ghost booooed"의 'booooo'와 대응되고, "A bird warbled"의 'b'에 대응되지만, "A goat grunted"내의 어느 부분과도 대응되지 않음

- `+`

  - 앞의 표현식이 1회 이상 연속으로 반복되는 부분과 대응됨
  - `{1,}`와 같은 의미
  - ex
    - `/a+/`는 "candy"의 'a'에 대응되고, "caaaaandy"의 모든 'a'들에 대응되지만, "cndy"내의 어느 부분과도 대응되지 않음

- `?`

  - 앞의 표현식이 0 또는 1회 등장하는 부분과 대응됨
  - `{0, 1}`와 같은 의미
  - ex
    - `/e?le?`는 "angel"의 'el'에 대응되고, "angle"의 'le'에 대응되고 또한 "oslo"의 'l'에도 대응됨
  - 만약 수량차(`*`, `+`, `?`, `{}`) 바로 뒤에 사용하면, 기본적으로 탐욕스럽던(가능한 한 많이 대응시킴) 수량자를 탐욕스럽지 않게(가능한 가장 적은 문자들에 대응시킴) 만듦
  - ex
    - `/\d+/`를 "123abc"에 적용시키면 "123"과 대응됨
    - `/\d+?/`를 같은 문자열에 적용시키면 오직 "1" 과만 대응됨
  - `x(?=y)`와 `x(?!y)` 항목에서 설명하는 바와 같이 사전 검증(lookahead assertion)을 위해서도 쓰임

- `.`

  - 개행 문자를 제외한 모든 단일 문자와 대응됨
  - ex
    - `/.n/`은 "nay, an apple is on the tree"에서 'an'과 'on'에 대응되지만, 'nay'에는 대응되지 않음

- `(x)`

  - 다음의 예제가 보여주는 것처럼 'x'에 대응되고 그것을 기억함. 괄호는 포획 괄호(capturing parentheses)라 불림

  - ex

    - `/(foo) (bar) \1 \2/`안의 '(foo)'와 '(bar)'는 문자열 "foo bar foo bar"에서 처음의 두 단어에 대응되고 이를 기억함. 패턴 내부의 `\1`와 `\2`는 문자열의 마지막 두 단어에 대응됨

      (`\n`패턴은 앞의 n번째 포획괄호에 대응된 문자열과 똑같은 문자열에 대응됨)

    - `\1`, `\2`, `\n`과 같은 문법은 정규식의 패턴 부분에서 사용됨.
    - 정규식의 치환 부분에서는 `$1`, `$2`, `$n`과 같은 문법이 사용됨
      - ex
        - 'bar foo'.replace( /(...) (...)/, '$2 $1')와 같이 사용되어야함
        - `$&`패턴은 앞에서 대응된 전체 문자열을 가리킴

- `(?:x)`

  - 'x'에 대응되지만 대응된 것을 기억하지 않음. 괄호는 비포획 괄호(non-capturing parentheses)라고 불리우고, 정규식 연산자가 같이 동작할 수 있게 하위 표현을 정의할 수 있음
    - ex
      - `/(?:foo){1, 2}/`인 경우 `{1, 2}`는 'foo'의 마지막 'o'에만 적용됨. 비포획 괄호가 같이 쓰일 경우, `{1, 2}`는 단어 'foo'전체에 적용됨

- `x(?=y)`

  - 오직 '`y`'가 뒤따라오는 '`x`'에만 대응됨 --> 이것을 `lookahead`라고 부름
  - ex
    - `/Jack(?=Sprat)`은 'Sprat'가 뒤따라오는 'Jack'에만 대응됨, 'Sprat'는 대응 결과가 아님
    - `/Jack(?=Sprat|Frost)/`는 'Sprat'또는 'Frost'가 뒤따라오는 'Jack'에만 대응됨, 'Sprat'와 'Frost'는 대응 결과가 아님

- `x(?|y)`

  - 'x'뒤에 'y'가 없는 경우에만 'x'에 일치함 --> 이것을 `negated lookahead`라고 부름
  - ex
    - `/\d+(?!\.)/`는 소숫점이 뒤따라오지 않는 숫자에 일치함
    - 정규식 `/\d+(?!\.)/.exec("3.141")`는 '3.141'이 아닌 '141'에 일치함

- `x|y`

  - 'x'또는 'y'에 대응됨
  - ex
    - `/green|red/`는 "green apple"의 "green"에 대응되고, "red apple"의 'red'에 대응됨

- `{n}`

  - 앞 표현식이 n번 나타나는 부분에 대응됨. n은 반드시 양의 정수여야 함
  - ex
    - `/a{2}/`는 "candy"의 'a'에는 대응되지 않지만, "caandy"의 모든 a와, "caaandy"의 첫 두 a에는 대응됨

- `{n, m}`

  - n과 m은 양의 정수이고, n <= m을 만족해야함
  - 앞 문자가 최소 n개, 최대 m개가 나타나는 부분에 대응됨
  - m이 생략된다면 m은 무한대로 취급됨.
  - ex 
    - `/a{1, 3}/`은 "cndy"에서 아무것에도 대응되지 않지만, "caandy"의 첫 두 a와 "caaaaandy"의 첫 세 a에 대응됨. "caaaaaaaaaandy"에서 더 많은 a들이 있지만, "aaa"에만 대응됨

- `[xyz]`

  - 문자셋(Character set)

  - 괄호 안의 어떤 문자(이스케이프 시퀀스(`/`)까지 포함)와도 대응됨

  - 점(`.`)이나 별표(`*`)같은 특수 문자는 문자셋 내부에서는 특수 문자가 아님.

    -> 이스케이프시킬 필요가 없음

  - 하이픈을 이용하여 문자의 범위를 지정할 수 있음
  - ex
    - 패턴`[a-d]`는 패턴 `[abcd]`와 똑같이 동작하여 `[brisket]`의 `[b]`에 일치, `[city]`의 `[c]`에 일치
    - `/[a-z.]+/`와 `/[\w.]+/`는 "test.i.ng" 전체 문자열이 일치함

- `[^xyz]`

  - 부정 문자셋(neated character set) 또는 보충 문자셋(complemented character set)
  - 괄호 내부에 등장하지 않는 어떤 문자와도 대응됨
  - 하이픈을 이용하여 문자의 범위를 지정할 수 있음
  - 일반적인 문자셋에서 작동하는 모든 것은 여기서도 작동함
  - ex
    - 패턴`[^abc]`는 패턴 `[^a-c]`와 동일함. 두 패턴은 "brisket"의 "r", "chop"의 "h"에 대응됨

- `[\b]`

  - 백스페이스(U+0008)에 대응됨
  - 백스페이스 문자 리터럴에 대응시키려면 대괄호("`[]`")를 이용해야만 함
  - *주의* : `/b`와 혼동 금지 

- `\b`

  - 단어 경계에 대응됨
  - 단어 경계 == 다른 '단어 문자'가 앞이나 뒤에 등장하지 않는 위치
  - 단어의 경계는 대응 결과에 포함되지 않음
  - 단어의 경계에 대응되는 문자열의 길이는 항상 0임
  - *주의* : 패턴`[/b]`와 혼동 금지
  - ex
    - `/\bm/`는 "moon"의 'm'에 대응됨
    - `/oo\b/`는 "moon"의 'oo'부분에 대응되지 않는데, 왜냐하면 'oo'를 뒤따라오는 'n'이 단어 문자이기 때문
    - `/oon\b/`는 "moon"의 'oon'에 대응됨, 왜냐하면 'oon'은 문자열의 끝이라서 뒤따라오는 단어 문자가 없기 때문
    - `/\w\b\w/`는 어떤 것에도 일치하지 않음. 왜냐하면 단어 문자는 절대로 비 단어 문자와 단어 문자 두 개가 뒤따라올 수 없기 때문

- `\B`

  - 단어 경계가 아닌 부분에 대응됨
    - 문자열의 첫 번째 문자가 단어 문자가 아닌 경우, 해당 문자의 앞 부분에 대응됨
    - 문자열의 마지막 문자가 단어 문자가 아닌 경우, 해당 문자의 뒷 부분에 대응됨
    - 두 단어 문자의 사이에 대응됨
    - 단어 문자가 아닌 두 문자 사이에 대응됨
    - 빈 문자열에 대응됨
  - 문자열의 시작 부분과 끝 부분은 단어가 아닌 것으로 간주됨
  - ex
    - `/\B../`는 "noonday"의 'oo'와 대응되며, `/y\B./`는 "possibly yesterday."의 'ye'와 대응됨

- `\cX`

  - 문자열 내부의 제어 문자에 대응됨
  - 여기서 X는 A에서 Z까지의 문자 중 하나
  - ex
    - `/\cM/`는 문자열에서 control-M(U+000D)에 대응됨

- `\d`

  - 숫자 문자에 대응됨. `[0-9]`와 동일함
  - ex
    - `/\d/`또는 `/[0-9]/`는 "B2 is the suite number"에서 '2'에 대응됨

- `\D`

  - 숫자가 아닌 문자에 대응됨. `[^0-9]`와 동일함
  - ex
    - `/\D/`또는 `/[^0-9]/`는 "B2 is the suite number"의 'B'에 대응됨

- `\f`

  - 폼피드 (U+000C) 문자에 대응됨

- `\n`

  - 줄 바꿈(U+000A) 문자에 대응됨

- `\r`

  - 캐리지 리턴(U+000D) 문자에 대응됨

- `\S`

  - 스페이스, 탭, 폼피드, 줄 바꿈 문자등을 포함한 하나의 공백 문자에 대응됨
  - `[ \f\n\r\t\v\u00a0\u1680\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]`와 동일
  - ex
    - `/\s\w*/`는 "foo bar."의 'bar'에 대응됨

- `\t`

  - 탭(U+0009) 문자에 대응됨

- `\v`

  - 수직 탭(U+000B) 문자에 대응됨

- `\w`

  - 밑줄 문자를 포함한 영숫자 문자에 대응됨
  - `[A-Za-z0-9_]`와 동일함 (여기에 대응되는 문자를 단어 문자라고 함)
  - ex
    - `/\w\`는 "apple"의 'a'에 대응되고, "$5.28"의 '5'에 대응되고, "3D"의 '3'에 대응됨

- `\W`

  - 단어 문자가 아닌 문자에 대응됨

  - `[^A-Za-z0-9_]`와 동일
  - ex
    - `/\W\` 또는 `.[^A-Za-z0-9_]/`는 "50%"의 '%'에 대응됨

- `\n`

  - 정규식 내부의 n번째 괄호에서 대응된 부분에 대한 역참조(n은 양의 정수)

- `\0`

  - 널(U+0000) 문자에 대응함.
  - *주의* : 다른 숫자를 뒤에 쓰면 8진 이스케이프 시퀀스가 됨 (`\0<digits>`이 8진 이스케이프 시퀀스이기 때문)

- `\xhh`

  - 코드가 hh(두 16진 숫자)인 문자에 일치

- `\uhhhh`

  - 코드가 hhhh(네 개의 16진 숫자)인 문자에 일치



### (3) 괄호를 사용하기

>  정규식 내부의 일부를 둘러싼 괄호는 해당 부분에서 대응된 문자열을 기억하는 효과를 가짐
>
> 기억된 문자열은 이후 패턴화된 부분 문자열 일치 사용하기에서 설명한 것처럼 다른 곳에서 사용하기 위하여 불러와질 수 있음

- ex
  - `/Chapter (\d+)\.\d*/`
    - 패턴의 일부분이 기억될 거라는 사실을 나타냄
    - 하나 이상의 숫자(`\d`는 숫자를 의미하고, `+`는 1개 이상을 의미함) 이후에 하나의 소숫점(`\`가 앞에 붙은 소숫점은 문자 그대로의 문자'.'에 대응됨을 나타냄)
    - 그 뒤 0개 이상의 숫자(`\d`는 숫자, `*`는 0개 이상을 의미)가 뒤따라오는 'Chapter'문자열에 대응됨
    - 괄호는 처음으로 일치하는 숫자 문자들을 기억하기 위하여 사용됨
- 부분 문자열을 대응시키면서도 해당 부분을 기억하지 않으려면, 괄호의 첫머리에 `?:`패턴을 사용하기



## 2) 정규식 사용하기

> 정규식은 `RegExp`, `test`, `exec`, `String`, `match`, `replace`, `search`, `split` 메소드와 함께 쓰임

- `exec`
  - 대응되는 문자열을 찾는 `RegExp` 메소드
  - 정보를 가지고 있는 배열을 반환함
  - 대응되는 문자열을 찾지 못했다면 `null`을 반환함
- `test`
  - 대응되는 문자열이 있는지 검사하는 `RegExp` 메소드
  - `true`나 `false`를 반환함
- `match`
  - 대응되는 문자열을 찾는 `RegExp`메소드
  - 정보를 가지고 있는 배열을 반환함
  - 대응되는 문자열을 찾지 못했다면 `null`을 반환함
- `search`
  - 대응되는 문자열이 있는지 검사하는 `String`메소드
  - 대응된 부분의 인덱스를 반환함
  - 대응되는 문자열을 찾지 못했다면 `-1`을 반환함
- `replace`
  - 대응되는 문자열을 찾아 다른 문자열로 치환하는 `String`메소드
- `split`
  - 정규식 혹은 문자열로 대상 문자열을 나누어 배열로 반환하는 `String`메소드



출처 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%EC%A0%95%EA%B7%9C%EC%8B%9D