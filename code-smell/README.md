# "코드 악취(Code Smell)" 란 무엇일까요? 🤢

> "코드 악취(Code Smell)"란 코드의 구조나 디자인에 **잠재적인 문제가 있는 흔한 증상을 가리키는 개념입니다**. 

코드에서 나는 악취는 코드의 품질을 저하시키고 유지보수를 어렵게 만들 수 있습니다. 이러한 악취들은 코드를 더 이해하기 어렵게 만들며, 버그 발생의 원인이 될 수 있습니다. 따라서 코드에서 나는 악취를 발견하고 이를 해결하는 것이 중요합니다.

## 악취 종류 😱

- 가변 데이터(Mutable Data)
- 거대한 클래스(Large Class)
- 기능 편애(Feature Envy)
- 기본형 집착(Primitive Obsession)
- 기이한 이름(Mysterious Name)
- 긴 매개변수 목록(Long Parameter List)
- 긴 함수(Long Functions)
- 내부자 거래(Insider Trading)
- 데이터 뭉치(Data Clumps)
- 데이터 클래스(Data Class)
- 뒤엉킨 변경(Divergent Change)
- 메시지 체인(Message Chains)
- 반복되는 switch문(Repeated Switches)
- 반복문(Loops)
- 산탄총 수술(Shotgun Surgery)
- 상속 포기(Refused Bequest)
- 서로 다른 인터페이스의 대안 클래스들(Alternative Classes with Different Interfaces)
- 성의 없는 요소(Lazy Element)
- 임시 필드(Temporary Field)
- 전역 데이터(Global Data)
- 주석(Comments)
- 중개자(Middle Man)
- 중복 코드(Duplicated Code)
- 추측성 일반화(Speculative Generality)


## Code smell 예시

다음은 일반적인 코드에서 나는 악취의 예시입니다:

1. 중복 코드(Duplicated Code): 같거나 비슷한 코드 블록이 여러 곳에 중복해서 나타나는 경우. 코드를 수정할 때 모든 중복 코드를 변경해야 하기 때문에 유지보수에 어려움을 초래합니다.

```js
function calculateAreaOfRectangle(width, height) {
  return width * height;
}

function calculateAreaOfSquare(side) {
  return side * side;
}
```

2. 긴 메서드(Long Method): 하나의 메서드가 너무 길고 복잡한 경우. 이해하기 어려운 코드를 만들고 유지보수가 어렵게 만듭니다.

```js
function complexCalculation(a, b, c, d) {
  // Very long and complex logic here
  // ...
}
```

3. 매직 넘버(Magic Number): 코드에서 직접적으로 사용되는 숫자 상수. 이해하기 어렵고 변경하기 어렵게 만듭니다.

```js
function calculateCircleArea(radius) {
  return 3.14 * radius * radius; // 3.14는 매직 넘버
}
```

4. 긴 매개변수 목록(Long Parameter List): 메서드의 매개변수가 너무 많은 경우. 매개변수의 개수가 많으면 메서드 호출과 관련된 이해와 유지보수가 어려워집니다.

```js
function createUser(name, age, email, address, phone, ...otherDetails) {
  // ...
}
```

5. 클래스의 크기가 너무 큼(Large Class): 클래스가 너무 많은 책임을 지고 있는 경우. 단일 책임 원칙을 위반하고 유지보수에 어려움을 초래합니다.

```js
class User {
  // 너무 많은 메서드와 속성들이 있는 큰 클래스
}
```

이러한 코드에서 나는 악취들은 코드의 품질을 저하시키고 유지보수를 어렵게 만드므로, 이러한 악취들을 발견하고 리팩토링하여 코드의 품질을 개선해야 합니다.