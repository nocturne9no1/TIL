# async/await의 동작원리를 살펴보자!

## 서론

지난 시간 `generator` 함수에 대해 살펴보며 함수의 실행을 일시중지/재개 할 수 있는 방법에 대해 알아보았습니다. 이번 시간에는 이 지식을 통해 `async/await` 의 동작원리에 대해 알아보겠습니다.



## 비동기를 동기처럼?

제네레이터 함수는 `next` 메서드와 `yield` 표현식을 사용하여 함수 호출자와 함수의 상태를 주고 받을 수 있다고 지난번 설명한 바 있습니다. 이러한 특징을 활용하면 `Promise` 를 사용한 비동기 처리를 동기 처럼 구현할 수 있습니다. 즉, 프로미스의 후속 처리 메서드 없이 비동기 처리 결과를 반환하도록 구현할 수 있는 것이죠!

```js
const async = (generatorFunc) => {
  const generator = generatorFunc();
  
  const onResolved = arg => {
    const result = generator.next(arg);
    
    return result.done
      ? result.value
      : result.value.then(res => onResolved(res));
  }
  return onResolved;
};

(async(function* fetchTodo() {
  const url = '요청하는 url';
  
  const response = yield fetch(url);
  const todo = yield response.json();
  console.log(todo);
})());
```

위 코드의 흐름 순서를 설명해보자면 다음과 같습니다.

1. async 함수가 호출되면 인수로 전달받은 제네레이터 함수 `fetchTodo` 호출하여 제네레이터 객체 생성

   → onResolved 함수 반환

   → onResolved 함수는 상위 스코프의 generator 변수를 기억하는 클로저

   → async 함수가 반환한 onResolved 함수를 즉시 호출하여 `const generator` 에서 생성한 제네레이터 객체의 `next` 메서드 처음 호출

2. `next` 메서드 처음 호출되면 `fetchTodo` 의 첫 번째 `yield` 문까지 실행

   → 이때 next 메서드가 반환한 이터레이터 리절트 객체의 done 프로퍼티 값이 false라면

   → 이터레이터 리절트 객체의 value 프로퍼티 값, 즉 첫 번째 yield 된 fetch(url) 함수가 반환한 프로미스가 resolve 한 Response 객체를 onResolved 함수에 인수로 전달하면서 재귀 호출

3. onResolved 함수에 인수로 전달된 Response 객체를 next 메서드에 인수로 전달하면서 next 메서드를 두 번째로 호출

   → 이때 next 메서드에 인수로 전달한 Response 객체는 제네레이터 함수 fetchTodo의 response 변수에 할당

   → 제네레이터 함수 fetchTodo 의 두 번째 yield 문까지 실행

4. `next` 메서드가 반환한 이터레이터 리절트 객체의 done 프로퍼티 값이 false라면 이터레이터 리절트 객체의 value 프로퍼티 값인 response.json 메서드가 반환한 프로미스가 resolve 한 todo 객체를 onResolved 함수에 인수로 전달하며 재귀 호출

5. onResolved 함수에 인수로 전달된 todo 객체를 next 메서드에 인수로 전달하면서 next 메서드를 세 번째로 호출

   → 이때 next 메서드에 인수로 전달한 todo 객체는 제네레이터 함수 fetchTodo의 todo 변수에 할당되고 제네레이터 함수 fetchTdoo 가 끝까지 실행

6. next 메서드가 반환한 이터레이터 리절트 객체의 done 프로퍼티 값이 true라면

   → 이터레이터 리절트 객체의 value 프로퍼티 값, 즉 제네레이터 함수 fetchTodo의 반환값인 undefined를 그대로 반환하고 처리 종료



언뜻보면 복잡해 보이지만 코드의 흐름을 한줄한줄 따라가다 보면 결국 ''`yield` 표현식을 할당받는 변수에 값이 할당되는 시점은 `yield` 표현식이 끝나는 시점이다!' 로 정리할 수 있습니다. 이를 기억하고 프로미스를 기반으로 동작하는 `async/await` 키워드를 통해 같은 로직을 구현해보겠습니다.



```js
async function fetchTodo() {
  const url = "요청 url";
  
  const response = await fetch(url);
  const todo = await response.json();
  console.log(todo);
}
```

WOW. 코드가 비약적으로 간단해 졌습니다. 하지만 같은 일을 처리하고 있죠. 가장 크게 보이는 차이점은 `yield` 표현식이 `await` 키워드로 바뀌었습니다. await의 우리말 표현인 '기다리다', 말그대로 await 키워드 뒤에 있는 일이 끝날 때 까지 기다린 뒤 변수에 할당하는 것입니다. Babel을 통해 위 코드를 ES5 버전으로 변환해보면 generator를 활용한 위의 코드와 비슷한 형식을 볼 수 있을 것입니다.

조금더 자세히 말하면 `await` 키워드는 Promise가 Settled(처리된) 상태가 될 때까지 대기하다가 Settled 상태가 되면 Promise가 resolve한 처리 결과를 반환합니다. 따라서 반드시 Promise 객체 앞에서 사용해야 합니다. 이러한 특징을 통해 비동기 처리를 마치 동기처럼 보이게 코드를 구성할 수 있는 것입니다.



## 마치며

지난 제네레이터부터 이번 `async/await` 까지 비동기 처리를 좀 더 쉽게 표현하기 위한 여정을 지나왔습니다. 이처럼 언어의 기능을 그 내부부터 이해하는 것은 그 언어와 좀 더 친해지는 기분을 느낄 수 있는 것 같습니다. 다음번에도 자바스크립트와 더 친해지기 위해 좀 더 그 코어로 들어 갈 수 있는 글로 찾아뵙겠습니다! 읽어주셔서 감사합니다 :) 