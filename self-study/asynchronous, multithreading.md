* ### [What is the difference between asynchronous programming and multithreading?](https://stackoverflow.com/questions/34680985/what-is-the-difference-between-asynchronous-programming-and-multithreading)
* ### [What is the difference between concurrency and parallelism?](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism)
* ### [Concurrency and Parallelism with Burgers - FastApi docs](https://fastapi.tiangolo.com/async/#concurrency-and-burgers)
--------------------------------  

의문점의 시작은 다음과 같다. Spring의 @Async를 적용한 메서드 실행 시 새로운 Thread가 위에서 작업이 처리가 되는 현상을 보았다.    
그래서 뭔가 이상했다. Asynchronous는 concurrency하기 때문에 single thread로 처리된다고 알고 있었기 때문이다.   
Thread가 새로 생긴다면 parallelism(multithreading)하게 되는건데, 나는 머릿속이 너무 복잡했다.       

우선 위의 링크들의 내용을 정리하면 다음과 같다. 아직까지 명확한 답은 모르겠다.   
* 첫번째 링크
  * asynchronous(비동기) : 작업이 처리되는 방식(e.g. synchronous, non-blocking)   
  * thread : 작업을 처리하는 주체
* 두번째 링크
  * concurrency : Interruptability(인터럽트 가능성)
  * parallelism : Independentability(독립성)
* 세번째 링크(결론)
  * asynchronous 작업은 concurrency(single thread)할 수도 있고, parallelism(multi thread)할 수도 있다???   
    언어마다 구현 방법이 다르다? node.js == concurrency, java == parallelism ???
