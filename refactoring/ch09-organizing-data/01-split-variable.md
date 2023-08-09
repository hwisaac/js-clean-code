"변수 쪼개기(Split Variable)"는 코드 리팩토링 기법 중 하나로, 하나의 변수가 두 가지 이상의 역할을 수행할 경우, 각 역할에 대해 별도의 변수를 사용하는 것을 의미합니다.

변수가 한 번만 할당되고 그 이후에는 변경되지 않는다면, 그 변수가 무엇을 의미하는지 이해하기 쉬워집니다. 이런 원칙은 "변수는 불변이어야 한다"는 함수형 프로그래밍의 원칙과도 일맥상통합니다.

예를 들어, 아래와 같은 코드가 있다고 가정해봅시다.

```js
let temp = 2 * (height + width);
console.log(`Perimeter: ${temp}`);
temp = height * width;
console.log(`Area: ${temp}`);
```

위의 코드에서 `temp` 변수는 두 가지 역할을 수행하고 있습니다. 먼저 주어진 높이와 너비로 사각형의 둘레를 계산하고, 그 다음에는 같은 높이와 너비로 사각형의 넓이를 계산합니다. "변수 쪼개기"를 통해 이 두 계산을 위한 별도의 변수를 사용하면 다음과 같이 됩니다.

```js
const perimeter = 2 * (height + width);
console.log(`Perimeter: ${perimeter}`);
const area = height * width;
console.log(`Area: ${area}`);
```

이제 `perimeter`와 `area`라는 두 변수는 각각 한 가지 역할만 수행하므로, 코드를 이해하기가 더 쉬워졌습니다. 또한, 이들은 불변성을 가지므로, 코드를 추적하고 디버깅하는 것이 더 쉬워집니다.