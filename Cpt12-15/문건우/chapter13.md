# 제 13장. 스코프

---

## 스코프란?

- 모든 식별자(변수 이름, 함수 이름)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 이를 스코프라 한다.

```javascript
var x = "global";

function foo() {
  var x = "local";
  console.log(x); // local
}

foo();

console.log(x); // global
```

---

### 스코프의 종류

- 스코프는 전역 스코프와 지역 스코프로 구분된다.
  - 전역 스코프: 코드의 가장 바깥 영역, 전역에 선언된 변수는 전역 스코프를 갖는다.
  - 지역 스코프: 함수 내부, 지역에 선언된 변수는 지역 스코프를 갖는다.
- 전역 변수는 어디서든지 참조할 수 있다.
- 지역 변수는 자신이 선언된 지역과 하위 지역에서만 참조할 수 있다.

### 스코프 체인

- 스코프 체인이란 스코프가 계층적으로 연결된 것을 말한다.
- 아래 이미지에서 스코프 체인은 최상위 스코프인 전역 스코프, 전역에서 선언된 outer 함수의 지역 스코프, outer 내부에서 선언된 inner 함수의 지역 스코프 로 이뤄졌다. - outer 함수가 만든 지역 스코프는 inner 함수가 만든 지역 스코프의 상위 스코프이다. - outer 함수의 지역 스코프의 상위 스코프는 전역 스코프이다. - 이처럼 모든 스코프가 하나의 계층적 구조로 연결되며 모든 지역 스코프의 최상위 스코프는 전역 스코프이다.
  ![스코프 체인](https://velog.velcdn.com/images%2Fminj9_6%2Fpost%2Fd0c1b672-0d8c-4a87-a13c-a4dfaa17a5d3%2Fimage.png)
- 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작해 상위 스코프 방향으로 이동하며 변수를 검색한다.

---

### 함수 레벨 스코프

- var 키워드로 선언된 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정한다. 함수 외부에서 var 키워드로 선언된 변수는 전역 변수가 된다.

```javascript
var x = 1;

if (true) {
  // var 키워드로 선언된 변수는 함수의 코드 블록을 지역 스코프로 인정한다.
  // 함수 밖에서 var 키워드로 선언된 변수는 '모두' 전역 변수다.
  // 따라서 x는 전역 변수다. 이미 선언된 전역 변수 x가 있으므로 x 변수는 중복 선언된다.
  // 이는 의도치 않게 변수 값이 변경되는 부작용을 발생시킨다.
  var x = 10;
}

console.log(x); // 10
```

```javascript
var i = 10;

// for 문에서 선언한 i는 전역 변수다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i < 5; i++) {
  console.log(i); // 0 1 2 3 4
}

// 의도치 않게 변수 값이 변경되었다.
console.log(i); // 5
```

### 렉시컬 스코프

- 렉시컬 스코프는 함수를 어디서 호출하는지가 아니라 어디에 선언하였는지에 따라 결정된다.
- 함수의 상위 스코프는 함수를 정의할 때 결정된다. 함수를 어디서 호출했는지는 스코프 결정에 아무런 의미를 주지 않는다.

```javascript
var x = 1;

function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

---
