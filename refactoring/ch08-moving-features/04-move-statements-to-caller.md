"문장을 호출한 곳으로 옮기기(Move Statements to Callers)"는 특정 함수가 자신의 목적 외의 일을 하는 경우, 그 부분을 함수에서 제거하고 함수를 호출하는 쪽으로 옮기는 리팩토링 기법을 의미합니다. 이는 함수의 기능을 더욱 명확히 하고, 불필요한 부작용(side effect)를 줄이는 데 도움이 됩니다.

예를 들어, 아래의 코드를 생각해봅시다.

```js
function getTotalCost(order) {
    const cost = order.quantity * order.itemPrice;
    console.log(`Total cost: ${cost}`);
    return cost;
}

function calculateDiscount(order) {
    const cost = getTotalCost(order);
    const discount = cost > 100 ? 0.05 : 0;
    return cost * discount;
}
```

위 코드에서 `getTotalCost` 함수는 계산된 비용을 반환하는 것뿐만 아니라 콘솔에 로그를 출력하는 부가적인 일을 하고 있습니다. 이 경우, `console.log` 문장을 `getTotalCost` 함수에서 제거하고 함수를 호출하는 곳으로 이동시키는 것이 좋을 수 있습니다.

```js
function getTotalCost(order) {
    return order.quantity * order.itemPrice;
}

function calculateDiscount(order) {
    const cost = getTotalCost(order);
    console.log(`Total cost: ${cost}`);
    const discount = cost > 100 ? 0.05 : 0;
    return cost * discount;
}
```

이제 `getTotalCost` 함수는 오직 비용 계산만을 담당하며, 로그 출력은 `calculateDiscount` 함수가 담당합니다. 이렇게 하면 각 함수의 책임이 더 명확해지고, 예상치 못한 부작용을 줄일 수 있습니다. 또한, 필요에 따라 같은 함수를 다른 목적으로 재사용할 수 있게 됩니다.