Question about REST Architecture
=================================
Rest Api에서 이미지를 처리하는 좋은 방법
--------------------------------
- 해당 내용은 stackoverflow의 비슷한 질문에 대한 답변을 참고함.   
(https://stackoverflow.com/questions/33279153/rest-api-file-ie-images-processing-best-practices)
- ~~이미지를 local 서버에 저장하는 경우~~
  - ~~이미지를 base64로 인코딩 하거나, multipart/form-data 형식으로 전송한다.~~
  - 이미지를 local 서버에 저장하는 것은 매우 비효율적이다. cloud를 사용해야 한다.
- 이미지를 cloud 서비스(s3, Google Cloud)에 저장하는 경우
  - 어느 시점에 cloud에 저장할지 결정해야 한다. 위의 답변에서는 사용자가 리소스를 생성하기 위해 이미지를 업로드 하는 그 시점에 cloud에 저장하는것이 좋다고 한다. 또한 업로드 한 이후에 리소스를 생성하지 않았다면 "할당되지 않은 이미지"가 생기게 되는데, 해당 경우는 그냥 무시하거나 가끔 cron으로 삭제 해주면 된다고 이야기 한다.
    - 그러면 javascript에서 직접 cloud로 전송해야 하는데, 보안적인 이슈가 없는지 궁금하다.
    - 이미지 파일이 아니라 영상일 경우에는 크기가 크기 때문에 아무리 비동기로 처리된다고 하더라도 이슈가 있을것 같다.
  - cloud에 저장한 데이터에 대한 uri를 꼭 서버로 전달해주어야 한다.



POST와 PUT 둘다 create 시에 사용 가능함. 그러면 둘의 차이점은 무엇인가?
----------------------------------------------------------
- 위의 질문의 답변중 user/4/images 요청을 PUT을 사용하는것을 보고 궁금한 점이 생겨 조금 더 찾아보았고, 해당 답변을 참고하였음.    
(https://stackoverflow.com/questions/630453/what-is-the-difference-between-post-and-put-in-http)
- POST와 PUT 둘다 지원 할 필요는 없다. 설계에 알맞게 적용해야한다.
  - 이미 client가 생성할 리소스에 대한 uri를 명확히 인지하고 있고, client의 요청이 멱등해야 한다면 PUT을 사용해야 한다.
  - client가 uri에 대해 전혀 모른다면 POST를 사용해야 한다.
- 새로운 리소스가 다른 리소스와의 연관 관계가 'is' 일 경우에는 PATCH(일부) 혹은 PUT(전체)을 사용하고, 'has' 일 경우에는 POST 혹은 PUT을 사용한다.
