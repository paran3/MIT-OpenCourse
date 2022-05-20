### [What is the difference between asynchronous programming and multithreading?](https://stackoverflow.com/questions/34680985/what-is-the-difference-between-asynchronous-programming-and-multithreading)
--------------------------------
### [What is the difference between concurrency and parallelism?](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism)
--------------------------------
### [Concurrency and Parallelism with Burgers](https://fastapi.tiangolo.com/async/#concurrency-and-burgers)

의문점의 시작은 다음과 같다. Spring의 @Async를 적용한 메서드 실행 시 새로운 Thread가 위에서 작업이 처리가 되는 현상을 보았다.    
그래서 뭔가 이상했다. (@Async는 single thread로 처리되는 줄 알고 있었다...)   
Thread가 새로 생긴 다는 의미는 Multi Thread와 같은 형태로 처리되는 것이라면 결국 비슷한 개념이 되는걸까?  


하지만 위의 링크를 들어가서 읽어보면 답을 알 수 있다.    
* asynchronous : 작업이 처리되는 방식(e.g. synchronous, non-blocking)    
* thread : 작업을 처리하는 주체

이러한 관점의 차이가 존재한다.    
그래서 작업자와 작업으

