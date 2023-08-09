"함수 옮기기(Move Function)" 또는 "메소드 이동(Method Moving)"이라고도 불리는 이 리팩토링 기법은, 함수(또는 메소드)가 자신이 속한 클래스보다 다른 클래스와 더 많은 상호작용을 하거나, 다른 클래스와 더 강하게 연관되어 있는 경우 해당 함수를 그 클래스로 이동시키는 방법을 말합니다.

함수를 옮기는 주된 목적은 클래스의 책임을 명확히 분리하고, 코드의 가독성을 높이며, 유지보수를 용이하게 하는 것입니다.

아래 예시를 확인해봅시다.

```js
class Account {
    constructor(accountType) {
        this.accountType = accountType;
    }

    interestForAmount_days(amount, days) {
        return this.accountType.interestRate * amount * days / 365;
    }
}

class AccountType {
    constructor(interestRate) {
        this.interestRate = interestRate;
    }
}
```

위 코드에서 `interestForAmount_days` 함수는 `AccountType`의 `interestRate`를 사용하여 계산을 수행하고 있습니다. 이 함수는 `AccountType` 클래스와 더 밀접하게 연관되어 있는 것으로 보이므로, 이를 `AccountType` 클래스로 옮기는 것이 적절해보입니다.

```js
class Account {
    constructor(accountType) {
        this.accountType = accountType;
    }
}

class AccountType {
    constructor(interestRate) {
        this.interestRate = interestRate;
    }

    interestForAmount_days(amount, days) {
        return this.interestRate * amount * days / 365;
    }
}
```

이처럼 "함수 옮기기"를 통해 함수가 사용하는 데이터와 가장 밀접한 클래스에 위치하도록 하여, 코드의 구조를 개선하고 가독성을 향상시킬 수 있습니다.