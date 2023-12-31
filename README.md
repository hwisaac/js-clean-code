# Clean Code 

## 닌자 코드란 무엇인가요?

"닌자 코드"는 일반적으로 코딩 또는 프로그래밍 커뮤니티에서 사용되는 용어로, **특정한 사람(주로 원 저자)만이 이해할 수 있는 복잡하고 읽기 어려운 코드**를 말합니다. 이 용어는 일반적으로 부정적인 의미로 사용되며, 해당 코드는 다른 사람이 이해하거나 수정하기 어렵습니다.

닌자 코드는 효과적인 팀 작업이나 코드 재사용을 방해하며, 이는 프로젝트의 유지 보수를 어렵게 만듭니다. 따라서, 좋은 프로그래밍 실습에서는 일반적으로 닌자 코드를 피하려고 노력합니다. 

닌자 코드는 주로 다음과 같은 상황에서 발생합니다:

## 지나치게 간결한 코드

코드를 가능한 짧게 만드는 것은 좋지 않습니다. 이렇게 하면 코드를 이해하기 어렵게 만들고 유지 관리하기 어려워집니다. 예를 들어, 삼항 연산자 '?'를 너무 복잡하게 사용하면 코드를 읽는 사람들이 어떤 값이 할당되는지 이해하는 데 어려움을 겪을 수 있습니다.

```js
i = i ? i < 0 ? Math.max(0, len + i) : i : 0;
```

## 한 글자 변수

코드를 짧게 만들기 위해 단일 문자 변수 이름을 사용하는 것은 피해야 합니다. 이렇게 하면 변수를 찾기 어렵게 만들며, 변수의 의미를 이해하는 것도 어렵게 합니다. 예를 들어, `a`, `b`, `c`와 같은 변수는 코드에서 쉽게 사라질 수 있습니다.

```js
let a = 10;
let b = a + 5;
let c = a + b;
```

## 약어 사용

팀 규칙이 한 글자 또는 모호한 이름을 금지하면 이름을 줄여 약어를 만드는 것은 좋지 않습니다. 이렇게 하면 코드를 이해하기 어려워집니다.

```js
let lst = []; // list의 약어
let ua = navigator.userAgent; // userAgent의 약어
let brsr = getBrowser(); // browser의 약어
```

## 고수준 추상화

가장 추상적인 단어를 사용하여 이름을 지정하는 것은 피해야 합니다. 이렇게 하면 변수의 실제 의미를 알아내기 어렵게 만듭니다.

```js
let data = getValue();
let str = data.toString();
let value = calculateValue(str);
```

## 주의력 테스트

변수 이름을 유사하게 만드는 것은 코드를 읽는 사람들에게 혼란을 줍니다. 이렇게 하면 코드를 빠르게 읽는 것을 어렵게 만들며, 오타가 있을 경우 문제를 해결하는 데 많은 시간이 소요될 수 있습니다.

```js
let date = new Date();
let data = fetchData();
```

## 유사한 이름 재사용

동일한 것들에 대해 유사한 이름을 사용하는 것은 코드를 더 흥미롭게 만들지만, 이는 혼란을 일으킬 수 있습니다.

```js
function displayMessage(msg) {
    // ...
}

function showMessage(user) {
    // ...
}
```

## 이름 재사용

필요할 때만 새 변수를 추가하고, 가능한 한 기존의 이름을 재사용하는 것은 좋지 않습니다. 이렇게 하면 변수에 어떤 값이 들어 있는지, 그리고 그 값이 어디서 왔는지를 파악하기 어렵게 만듭니다.

```js
let value = 1;
value = value + 2;
```

## 밑줄 사용

변수 이름 앞에 밑줄 `_` 또는 `__`을 붙이는 것은 코드를 더 길고 읽기 어렵게 만들며, 다른 개발자가 밑줄의 의미를 파악하는 데 많은 시간을 소비하게 만듭니다.

```js
let _value = 1;
let __anotherValue = _value + 1;
```

## 외부 변수명과 중복

함수 내부와 외부에서 같은 이름의 변수를 사용하는 것은 좋지 않습니다. 이렇게 하면 함수 내부에 있는 로컬 변수가 외부 변수를 가리게 되며, 이로 인해 혼란이 발생할 수 있습니다.

```js
let user = authenticateUser();

function render() {
    let user = getUser();
    // ...
}
```

## 부가효과(side effect)가 있는 함수

변경 사항이 없어 보이는 함수가 실제로는 "부가효과"를 가지고 있는 경우, 이는 코드를 이해하는 것을 어렵게 만들고, 예상치 못한 결과를 초래하거나 버그를 만들어냅니다.

```js
function addItemToArray(item, arr) {
    arr.push(item); // arr는 외부에서 받은 배열로, 이 함수 내에서 변경하면 원본 배열에 영향을 미치므로 사이드 이펙트를 가집니다.
}

let myArray = [1, 2, 3];
addItemToArray(4, myArray);
console.log(myArray); // 출력: [1, 2, 3, 4]
```

## 여러 기능을 수행하는 함수

함수 이름에 쓰여 있는 것보다 더 많은 작업을 수행하는 함수를 작성하는 것은 좋지 않습니다. 이렇게 하면 코드 재사용을 방해하게 됩니다.

```js
function validateEmail(email) {
    let isValid = checkEmail(email);
    if (!isValid) {
        showMessage('Invalid email');
        email = getEmailAgain();
    }
    return email;
}
```