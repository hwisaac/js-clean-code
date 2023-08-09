"Replace Inline Code with Function Call"은 일반적인 코드 리팩토링 기법 중 하나로, 코드에서 반복적으로 등장하는 일련의 명령들을 별도의 함수로 정의하고, 그 함수를 호출함으로써 코드의 중복을 줄이는 기법을 의미합니다.

이 기법은 코드의 가독성과 유지 관리성을 향상시키며, 이해를 쉽게 하고, 오류 가능성을 줄이는데 도움이 됩니다. 또한, 이런 식으로 함수를 만들면 테스트도 용이해집니다.

예를 들어, 다음과 같은 코드가 있다고 가정해봅시다.

```js
function printPrice(order) {
    const basePrice = order.quantity * order.itemPrice;
    const discount = Math.max(order.quantity - 500, 0) * order.itemPrice * 0.05;
    const shipping = Math.min(basePrice * 0.1, 100);
    const price = basePrice - discount + shipping;

    console.log(`Price: ${price}`);
}

function printDiscount(order) {
    const basePrice = order.quantity * order.itemPrice;
    const discount = Math.max(order.quantity - 500, 0) * order.itemPrice * 0.05;
    const shipping = Math.min(basePrice * 0.1, 100);
    const price = basePrice - discount + shipping;

    console.log(`Discount: ${discount}`);
}
```

위의 코드에서 `printPrice`와 `printDiscount` 함수가 동일한 계산을 수행하고 있습니다. 이럴 때 "Replace Inline Code with Function Call" 기법을 적용하면 다음과 같이 됩니다.

```js
function calculateTotal(order) {
    const basePrice = order.quantity * order.itemPrice;
    const discount = Math.max(order.quantity - 500, 0) * order.itemPrice * 0.05;
    const shipping = Math.min(basePrice * 0.1, 100);
    return basePrice - discount + shipping;
}

function printPrice(order) {
    const price = calculateTotal(order);
    console.log(`Price: ${price}`);
}

function printDiscount(order) {
    const price = calculateTotal(order);
    console.log(`Discount: ${price}`);
}
```

이제 `calculateTotal`라는 별도의 함수로 중복된 계산 로직을 추출했으므로, `printPrice`와 `printDiscount` 함수는 각각의 목적에만 집중할 수 있게 되었습니다. 이런 식으로 코드를 리팩토링하면, 같은 계산이 다른 곳에서도 필요할 경우 `calculateTotal` 함수를 재사용할 수 있고, 계산 방법이 변경되면 이 함수만 수정하면 되므로 유지보수도 용이해집니다.