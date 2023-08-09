"문장 슬라이드하기(Slide Statements)"는 코드 리팩토링 기법 중 하나로, 관련된 코드를 가까이 모으는 방법을 말합니다. 이 기법은 코드의 가독성을 높이고 이해를 돕는 데 도움이 됩니다.

함수 내부에서 문장들의 위치를 바꾸는 것은 쉽지만, 이러한 작은 변경들이 함수의 가독성과 이해도를 크게 향상시킬 수 있습니다. 연관된 동작들이 함께 위치하면 코드를 읽는 사람은 그 관계를 더 쉽게 이해할 수 있으며, 결과적으로 전체적인 코드 이해도가 향상됩니다.

예를 들어, 아래와 같은 코드가 있다고 가정해 봅시다.

```js
let mealPrice = getMealPrice();
let discount = getDiscount();
let deliveryPrice = getDeliveryPrice();

console.log(`Meal price: ${mealPrice}`);
console.log(`Discount: ${discount}`);

mealPrice = mealPrice - discount;

console.log(`Delivery price: ${deliveryPrice}`);
console.log(`Total: ${mealPrice + deliveryPrice}`);
```

위의 코드에서 할인 적용 후의 식사 가격을 계산하는 문장과 그것을 출력하는 문장이 분리되어 있습니다. "문장 슬라이드하기" 기법을 적용하면 이를 가까이 모을 수 있습니다.

```js
let mealPrice = getMealPrice();
let discount = getDiscount();
mealPrice = mealPrice - discount;

console.log(`Meal price: ${mealPrice}`);
console.log(`Discount: ${discount}`);

let deliveryPrice = getDeliveryPrice();
console.log(`Delivery price: ${deliveryPrice}`);
console.log(`Total: ${mealPrice + deliveryPrice}`);
```

이제 할인이 적용된 식사 가격에 관련된 코드들이 모여 있으므로, 그 계산과정을 이해하기 쉬워졌습니다. 이처럼 "문장 슬라이드하기" 기법은 코드의 가독성을 높이고 이해를 돕는데 큰 도움을 줍니다.