"특이 케이스 추가하기(Introduce Special Case)"는 특정 상황에 대한 처리를 위해 새로운 특별한 객체나 값 등을 도입하는 리팩토링 기법을 말합니다. 이 기법은 일반적인 조건 처리를 특정 상황에 대해 보다 명시적으로 처리할 수 있도록 도와줍니다.

일반적으로 조건문이나 예외 처리를 사용하여 특이한 상황을 처리할 수 있지만, 이러한 접근 방식은 코드를 복잡하게 만들 수 있습니다. 또한 특이한 상황을 처리하는 코드가 여러 곳에 중복되어 있을 수 있습니다.

"특이 케이스 추가하기"를 적용하면 이러한 문제를 해결할 수 있습니다. 특이한 상황에 대해 특별한 객체나 값 등을 도입하여 일반적인 처리와 구분할 수 있게 됩니다.

간단한 예제로 설명해보겠습니다. 우리는 사용자가 속한 팀에 따라 할인율을 계산하는 함수가 있다고 가정해봅시다.

```js
function calculateDiscount(user) {
  let discount = 0;
  if (user.team === 'VIP') {
    discount = 0.3;
  } else if (user.team === 'Premium') {
    discount = 0.2;
  } else if (user.team === 'Standard') {
    discount = 0.1;
  }
  return discount;
}
```

위 코드에서는 특정 팀에 따라 할인율을 계산하고 있습니다. 이제 "특이 케이스 추가하기"를 적용하여 특정 팀이 아닌 경우를 특별히 처리하는 객체를 도입하겠습니다.

```js
class SpecialTeam {
  getDiscount() {
    return 0.05;
  }
}

function calculateDiscount(user) {
  if (user.team === 'VIP') {
    return 0.3;
  } else if (user.team === 'Premium') {
    return 0.2;
  } else if (user.team === 'Standard') {
    return 0.1;
  } else {
    return new SpecialTeam().getDiscount();
  }
}
```

이제 팀이 'VIP', 'Premium', 'Standard'에 해당하지 않는 경우를 위해 `SpecialTeam`이라는 특이 케이스 객체를 사용하고 있습니다. 이 객체는 특별한 상황에 대한 처리를 담당하고, 이로 인해 코드가 더 명확해지고 가독성이 향상됩니다. 또한 특이 케이스 처리를 객체에 위임하므로 중복이 제거되고 코드의 유지보수성이 높아집니다.