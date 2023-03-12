# setTimeout / setInterval 관련 사항

**브라우저 환경에서 실제 대기 시간은 0이 아닙니다.**

브라우저는 [HTML5 표준](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#timers)에서 정한 중첩 타이머 실행 간격 관련 제약을 준수합니다. 해당 표준엔 "다섯 번째 중첩 타이머 이후엔 대기 시간을 최소 4밀리초 이상으로 강제해야 한다."라는 제약이 명시되어있습니다.

예시를 보며 이 제약 사항을 이해해봅시다. 예시 내 `setTimeout`은 지연 없이 함수 run을 다시 호출할 수 있게 스케줄링 되어 있습니다. 배열 `times`에는 실제 지연 간격에 대한 정보가 기록되도록 해놓았는데, 배열 times에 어떤 값이 저장되는지 알아봅시다.



```javascript
let start = Date.now();
let times = [];

setTimeout(function run() {
  times.push(Date.now() - start); // 이전 호출이 끝난 시점과 현재 호출이 시작된 시점의 시차를 기록

  if (start + 100 < Date.now()) alert(times); // 지연 간격이 100ms를 넘어가면, array를 얼럿창에 띄워줌
  else setTimeout(run); // 지연 간격이 100ms를 넘어가지 않으면 재스케줄링함
});

// 출력창 예시:
// 1,1,1,1,9,15,20,24,30,35,40,45,50,55,59,64,70,75,80,85,90,95,100
```



앞쪽 타이머들은 스펙에 적힌 것처럼 지연 없이 바로 실행됩니다. 그런데 다섯 번째 중첩 타이머 이후엔 지연 간격이 4밀리초 이상이 되어 `9, 15, 20, 24...`와 같은 값이 저장되는 것을 확인할 수 있습니다.

이런 제약은 `setTimeout`뿐만 아니라 `setInterval`에도 적용됩니다. `setInterval(f)`도 처음 몇 번은 함수 `f`를 지연 없이 실행하지만, 나중엔 지연 간격을 4밀리초 이상으로 늘려버립니다.

이는 오래전부터 있던 제약인데, 구식 스크립트 중 일부는 아직 이 제약에 의존하는 경우가 있어서 명세서를 변경하지 못하고 있는 상황입니다.

한편, 서버 측엔 이런 제약이 없습니다. Node.js의 [process.nextTick](https://nodejs.org/api/process.html)과 [setImmediate](https://nodejs.org/api/timers.html)를 이용하면 비동기 작업을 지연 없이 실행할 수 있습니다. 위에서 언급된 제약은 브라우저에 한정됩니다.

아시다시피 브라우저는 시간이 오래 걸리든 아니든 상관없이 현재 작업 중인 태스크가 끝나야 DOM 변경분을 화면에 렌더링해줍니다.