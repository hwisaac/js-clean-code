"함수 추출하기" (Extract Function)라는 리팩토링 기법은 코드의 특정 부분이 전체 중에 과도하게 크거나 한 가지 이상의 작업을 수행하는 경우에 사용되는 방법입니다. 이 기법은 코드의 가독성을 높이고 재사용성을 향상시키며, 각 함수는 한 가지 작업만 수행하도록 만듭니다.

이 기법을 사용하면 다음과 같은 장점을 얻을 수 있습니다:

1. 코드의 명확성: 함수는 특정 작업을 수행하는 코드의 모음이므로, 각 함수는 코드의 특정 부분이 어떤 작업을 수행하는지를 명확하게 만듭니다.
2. 코드 재사용: 한 번 정의된 함수는 필요할 때마다 다시 호출할 수 있습니다.
3. 유지 관리의 용이성: 각 함수가 한 가지 작업만 수행하므로, 문제가 발생한 경우 문제를 쉽게 찾고 수정할 수 있습니다.

"함수 추출하기"에 대한 더 간단한 예시를 들어보겠습니다. JavaScript 코드를 사용해 설명하겠습니다.

변경 전 코드:

```js
function sayHello() {
    const date = new Date();
    const hours = date.getHours();

    if (hours < 12) {
        console.log("Good morning!");
    } else if (hours < 18) {
        console.log("Good afternoon!");
    } else {
        console.log("Good evening!");
    }
}
```

위 코드에서 시간을 기반으로 인사말을 결정하는 로직을 별도의 함수로 추출해봅시다.

변경 후 코드:

```js
function sayHello() {
    const greeting = getGreetingBasedOnTime();
    console.log(greeting);
}

function getGreetingBasedOnTime() {
    const date = new Date();
    const hours = date.getHours();

    if (hours < 12) {
        return "Good morning!";
    } else if (hours < 18) {
        return "Good afternoon!";
    } else {
        return "Good evening!";
    }
}
```

이렇게 변경하면 `getGreetingBasedOnTime` 함수를 `sayHello` 외의 다른 곳에서도 재사용할 수 있게 되고, `sayHello` 함수도 더 간결하게 만들 수 있습니다. 또한, 각 함수가 어떤 작업을 하는지 더 명확히 알 수 있게 됩니다.