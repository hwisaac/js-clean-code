"조건문 분해하기(Decompose Conditional)"는 코드의 가독성을 향상시키기 위한 리팩토링 기법 중 하나입니다. 이 기법은 복잡한 조건문을 더 단순한 형태로 분해하는 것을 목표로 합니다.

복잡한 조건문이나 표현식은 코드를 이해하는데 방해가 될 수 있습니다. 이런 경우, 조건문을 분해하고 적절한 이름을 가진 함수로 추출함으로써 코드의 가독성을 향상시킬 수 있습니다.

좀 더 간단한 예제를 사용하여 "조건문 분해하기"에 대해 설명해 드리겠습니다.

예를 들어, 나이에 따른 할인율을 결정하는 함수가 있다고 가정해 봅시다.

```js
function getDiscount(age) {
    if (age < 14 || age > 65) {
        return 0.5;
    } else {
        return 0.1;
    }
}
```

위 코드에서는 나이가 14세 미만이거나 65세 초과인 경우 할인율을 50%로, 그렇지 않은 경우에는 10%로 설정하고 있습니다.

"조건문 분해하기"를 적용하면, 다음과 같이 코드를 리팩토링할 수 있습니다.

```js
function getDiscount(age) {
    if (isEligibleForHalfDiscount(age)) {
        return 0.5;
    } else {
        return 0.1;
    }
}

function isEligibleForHalfDiscount(age) {
    return age < 14 || age > 65;
}
```

위의 리팩토링에서는 복잡한 조건문을 `isEligibleForHalfDiscount`라는 별도의 함수로 분리하였습니다. 이렇게 하면 해당 조건이 무엇을 의미하는지를 더 명확하게 이해할 수 있습니다. 또한, 이 조건을 다른 곳에서도 재사용할 수 있게 되었습니다.