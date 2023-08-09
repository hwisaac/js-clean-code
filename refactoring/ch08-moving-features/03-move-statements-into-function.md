"Move Statements into Function"은 리팩토링 기법 중 하나로, 반복적으로 사용되는 코드 스니펫이 있을 때, 이를 별도의 함수로 만들어서 재사용하는 기법을 의미합니다. 이 기법은 코드의 중복을 줄이고 가독성을 높이며 유지보수를 쉽게 하는데 도움이 됩니다.

예를 들어, 주어진 코드에서 같은 계산이 여러 위치에서 발생한다고 가정해봅시다.

```js
function printInvoice(order) {
    const basePrice = order.quantity * order.itemPrice;
    const discount = Math.max(order.quantity - 500, 0) * order.itemPrice * 0.05;
    const shipping = Math.min(basePrice * 0.1, 100);
    console.log(basePrice - discount + shipping);
}

function printStatement(order) {
    const basePrice = order.quantity * order.itemPrice;
    const discount = Math.max(order.quantity - 500, 0) * order.itemPrice * 0.05;
    const shipping = Math.min(basePrice * 0.1, 100);
    console.log(`Base: ${basePrice}, Discount: ${discount}, Shipping: ${shipping}, Total: ${basePrice - discount + shipping}`);
}
```

위에서 `printInvoice`와 `printStatement` 함수 모두에서 동일한 계산이 이루어지고 있습니다. 이럴 때 "Move Statements into Function" 기법을 사용하여 중복을 제거할 수 있습니다.

```js
function calculateTotal(order) {
    const basePrice = order.quantity * order.itemPrice;
    const discount = Math.max(order.quantity - 500, 0) * order.itemPrice * 0.05;
    const shipping = Math.min(basePrice * 0.1, 100);
    return basePrice - discount + shipping;
}

function printInvoice(order) {
    console.log(calculateTotal(order));
}

function printStatement(order) {
    const total = calculateTotal(order);
    console.log(`Total: ${total}`);
}
```

이제 중복된 계산 코드가 `calculateTotal` 함수로 이동되었으며, `printInvoice`와 `printStatement` 함수에서는 이 함수를 호출하여 필요한 값을 얻습니다. 이렇게 하면 코드의 중복을 줄이고 가독성을 높일 수 있습니다. 또한, 계산 방법이 변경되어야 할 경우에는 `calculateTotal` 함수만 수정하면 되므로 유지보수도 쉬워집니다.