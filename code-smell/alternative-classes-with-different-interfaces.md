> 서로 다른 인터페이스의 대안 클래스들(Alternative Classes with Different Interfaces) 악취는 **비슷한 기능을 수행하는 여러 클래스들이 각각 다른 인터페이스를 가지고 있어서 클라이언트 코드가 이를 처리하기 어려운 상황**을 의미합니다.

일반적으로 객체 지향 프로그래밍에서는 다형성을 활용하여 여러 클래스들을 하나의 추상화된 인터페이스로 다루어야 합니다. 하지만 때로는 비슷한 기능을 수행하는 클래스들이 각각 다른 인터페이스를 가지고 있어서 클라이언트 코드가 각 클래스를 개별적으로 다뤄야 하는 상황이 발생합니다. 이런 상황에서 서로 다른 인터페이스의 대안 클래스들 악취가 발생합니다.

이 악취는 코드의 복잡성을 증가시키고, 유지 보수성을 저하시키며, 유연성을 감소시키는 원인이 됩니다. 클라이언트 코드가 각 클래스를 개별적으로 다뤄야 하므로, 새로운 클래스가 추가되거나 기존 클래스가 변경되는 경우 클라이언트 코드를 모두 수정해야 하는 번거로움이 발생합니다. 또한 각 클래스의 다른 인터페이스로 인해 코드의 유연성이 저하되어 확장이 어려워질 수 있습니다.

서로 다른 인터페이스의 대안 클래스들 악취를 해결하기 위해서는 비슷한 기능을 수행하는 클래스들을 하나의 추상화된 인터페이스로 통일하는 리팩토링을 수행해야 합니다. 인터페이스를 추상화하고, 다형성을 활용하여 클라이언트 코드가 동일한 방식으로 다양한 클래스를 다룰 수 있도록 설계하는 것이 좋습니다.

예를 들어, 서로 다른 인터페이스의 대안 클래스들 악취를 가진 코드를 살펴보겠습니다:

```js
class Car {
  startEngine() {
    // 자동차 시동 켜기
  }

  drive() {
    // 자동차 운전하기
  }
}

class Bicycle {
  pedal() {
    // 자전거 페달 밟기
  }

  ride() {
    // 자전거 타기
  }
}
```

위의 예시에서 `Car` 클래스와 `Bicycle` 클래스는 비슷한 기능을 수행하지만, 각각 다른 인터페이스를 가지고 있습니다. 이런 경우 클라이언트 코드가 각 클래스를 개별적으로 다뤄야 하는 상황이 발생할 수 있습니다.

서로 다른 인터페이스의 대안 클래스들 악취를 해결하기 위해 공통된 인터페이스를 추출하고 다형성을 활용하여 클라이언트 코드가 동일한 방식으로 다양한 클래스를 다룰 수 있도록 리팩토링할 수 있습니다:

```js
class Vehicle {
  start() {
    // 차량 시동 켜기 또는 자전거 페달 밟기
  }

  drive() {
    // 차량 운전하기 또는 자전거 타기
  }
}
```

위의 예시에서 `Car` 클래스와 `Bicycle` 클래스를 `Vehicle` 클래스로 통합하여 공통된 인터페이스를 추상화하였습니다. 이렇게 함으로써 서로 다른 인터페이스의 대안 클래스들 악취를 해결하고, 코드의 유지 보수성과 유연성을 향상시킬 수 있습니다. 클라이언트 코드는 이제 `Vehicle` 클래스를 통해 다양한 차량과 자전거를 다룰 수 있게 되었습니다.