"변수 추출하기"(Extract Variable)는 표현식의 결과나 표현식 자체를 새로운 변수에 할당하는 리팩토링 기법입니다. 이 기법은 주로 복잡한 표현식을 분해하거나 의미를 명확하게 하기 위해 사용됩니다.

다음과 같은 JavaScript 코드를 가정해봅시다:

```js
function calculateTotalPrice(quantity, price) {
    return quantity * price + (quantity * price * 0.1);
}
```

위 코드에서 `quantity * price * 0.1`은 10%의 세금을 의미합니다. 하지만 이를 처음 보는 사람은 이해하기 어려울 수 있습니다. 이런 경우에 "변수 추출하기"를 사용하여 코드를 명확하게 만들 수 있습니다:

```js
function calculateTotalPrice(quantity, price) {
    const basePrice = quantity * price;
    const tax = basePrice * 0.1;
    return basePrice + tax;
}
```

위 코드에서는 `basePrice`와 `tax`라는 새로운 변수를 도입하여, 각각이 무엇을 의미하는지 명확하게 만들었습니다. 이렇게 하면 코드를 읽는 사람이 이해하기 쉬워지며, 유지보수도 더 쉬워집니다.

"변수 추출하기" 기법은 코드의 가독성을 높이고, 복잡한 표현식을 분해하여 코드의 목적과 의도를 더 명확하게 표현하는데 사용됩니다. 그러나 너무 많은 변수를 도입하면 반대로 코드를 복잡하게 만들 수 있으므로, 적절히 사용해야 합니다.