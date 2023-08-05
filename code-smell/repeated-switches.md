> 반복되는 `switch` 문은 소프트웨어 개발에서 발생하는 코드 냄새(Code Smell) 중 하나로, 동일한 `switch` 문 또는 유사한 조건문이 여러 곳에서 반복적으로 사용되는 상황을 가리킵니다. 이는 중복 코드를 발생시키고 코드의 가독성과 유지보수성을 저하시키는 원인이 됩니다.

반복되는 `switch` 문은 일반적으로 여러 곳에서 같은 유형의 조건을 체크해야 할 때 발생할 수 있습니다. 예를 들어, 다양한 상황에서 동일한 타입의 객체를 생성하거나 다른 동작을 수행해야 할 때 각각의 상황을 `switch` 문으로 구분하는 경우가 있습니다.

이러한 상황에서는 코드가 불필요하게 중복되어 유지보수를 어렵게 만들고, 새로운 상황이 추가될 때마다 모든 `switch` 문을 수정해야 하는 번거로움이 발생합니다. 또한, 코드가 중복되므로 버그 발생 가능성이 높아지고, 가독성이 저하되어 코드의 이해가 어려워집니다.

반복되는 `switch` 문을 해결하기 위해서는 일반적으로 다형성(Polymorphism)을 활용하는 리팩토링을 수행합니다. 다형성을 사용하면 각각의 상황을 별도의 클래스나 함수로 추상화하여 중복 코드를 제거하고, 새로운 상황이 추가되더라도 해당 클래스나 함수만 추가하면 되므로 코드의 확장성과 유지보수성이 향상됩니다.

예시를 통해 설명해보겠습니다.

**반복되는 switch 문 (Code Smell 상태)**

```js
function calculateShippingCost(order) {
  switch (order.shippingMethod) {
    case 'standard':
      return order.total * 0.05;
    case 'express':
      return order.total * 0.1;
    case 'overnight':
      return order.total * 0.2;
    default:
      throw new Error('Invalid shipping method');
  }
}

function calculateTax(order) {
  switch (order.shippingMethod) {
    case 'standard':
      return order.total * 0.1;
    case 'express':
      return order.total * 0.15;
    case 'overnight':
      return order.total * 0.2;
    default:
      throw new Error('Invalid shipping method');
  }
}
```

위 코드에서 `order` 객체의 `shippingMethod`를 체크하는 `switch` 문이 두 개의 함수에서 반복적으로 사용되고 있습니다.

**해결한 코드 (반복되는 switch 문 해결)**

```js
class ShippingCalculator {
  calculateShippingCost(order) {
    // ... calculate shipping cost based on order ...
  }

  calculateTax(order) {
    // ... calculate tax based on order ...
  }
}
```

해결한 코드에서는 `ShippingCalculator` 클래스를 도입하여 `calculateShippingCost`와 `calculateTax` 함수를 클래스의 메소드로 추상화하였습니다. 이제 각 함수의 내부 구현은 해당 클래스 내에서 독립적으로 관리됩니다. `shippingMethod` 체크는 클래스 내부에서 이루어지고, 이로 인해 중복 코드가 제거되고 가독성과 유지보수성이 향상됩니다.

새로운 상황이 추가되더라도 `ShippingCalculator` 클래스 내에서만 해당 상황을 처리하면 되므로 기존 코드를 건드리지 않아도 됩니다. 이렇게 하면 코드의 확장성이 높아지고, 반복되는 `switch` 문으로 인한 중복 코드를 피할 수 있습니다.