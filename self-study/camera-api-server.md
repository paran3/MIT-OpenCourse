Camera Analyze Server (prototype)
=====================
Api
---
config api (CRUD) : regist camera information(id, default image - base image for analyze, coordinates).    
analyze api : analyze image which is uploaded by client.
- camera config api : 카메라(cctv) 등록.
  - create
    - request
      - cameraId
      - config image
      - coordinate(leftTop, rightTop, leftBottom, rightBottom)
      - width
      - height
      - description
    - response : 201 created(location : uri)
  - get(전체 카메라 조회)
    - request
    - response
      - cameraId List
- camera analyze api : 등록된 카메라의 config image와 image(분석 대상)를 비교하여 사물과 사물 혹은 사물과 벽 사이의 거리를 측정한다.
  - image
    - create
      - request
        - camearId
        - image
      - response
        - image
  - video
    - create
      - request
        - cameraId
        - video
      - response : 201 created(location : uri)

Design Pattern
--------------
- model
  - dto : controller <-> service layer 간에 전달되는 데이터 오브젝트
  - dao : service <-> database layer 간에 전달되는 데이터 오브젝트
  - vo : view <-> controller 간에 전달되는 데이터 오브젝트
- service : service의 역할(비지니스 로직)
- rest_api.py : controller의 역할
- view.py : view의 역할  

ISSUE
-----
- venv setting
- media file(image,video) request and response
  - javascript의 fetch 메서드를 사용하는데, 파일이 어떻게 변환되어서 전달되고, 전달 받아서 어떻게 처리해야 하는지 정학히 알지 못한다.
  - 쉽게 사용 가능한 라이브러리를 찾아봐야 한다.
  - 이미지를 바이너리 형태로 저장 하는것은 좋지않다.
- flask
  - 어떠한 이점이 있는지 모르겠다. 
  - spring을 사용하다보니 기본적으로 제공되지 않는 기능들이 너무 답답하게 느껴졌다.
  - orm을 외부 라이브러리를 사용해야 하는것이 불편했다.(해당 프로젝트는 아직 orm이 적용되어 있지 않음)
  - Response 오브젝트를 어떻게 사용해야 하는지 아직도 모르겠다.
  - fast api를 사용하거나 node로 개발하는것은 어떠한 이점이 있는지 파악해봐야 한다.
- nginx, gunicorn 적용
- design pattern
  - 개발 속도에 이점이 있는 디자인 패턴이 무엇인지 알아야 한다.
  - mvc패턴이 개발 속도가 빠른것 같지는 않다.(아닐수도 있음)
  - 디자인 패턴보다는 어떤 framework을 사용하는지가 더 중요할 수 있다.
- frontend
  - html, javascript 구조를 어떻게 잡아야하는지 전혀 모르겠다. 그렇기에 당연히 소스코드가 뒤죽박죽 엉켜있다.
- database
  - 개발 속도를 빠르게 하기 위하여 sqlite를 사용하였지만, 추후에는 postgresql로 변경하거나 이미지를 저장하기 용이한 database aws(s3)를 선택해야 한다.



solution
--------
- venv
  - venv 생성 : python -m venv (가상환경 디렉토리 이름)
  - venv 활성화 : (가상환경 디렉토리 이름)/Scripts/activate.bat (윈도우) / source (가상환경 디렉토리 이름)/bin/activate (Linux)
  - 패키지 리스트 생성 : pip freeze > requirements.txt
  - 패키지 리스트 설치 : pip install -r requirements.txt
- media file(image,video) request and response
  - ~~media file 자체를 response에 포함시키는것이 아니라. 어찌됐든 자원이 생성된것이기 때문에 201 created를 응답주면서 location에 uri를 포함시켜 응답을 주고, 클라이언트에서는 해당 uri로 링크를 걸면 되는것 아닌가?~~
  - 자세한 설명은 링크 참고(https://github.com/paran3/ArchitectureStudy/blob/main/backend/rest/README.md) 
- camera, analyze image 생성시에 사용하는 Http Method
  - camera_analyze_server의 api 설게 과정에서 camera 리소스를 생성한 이후에 analyze image를 서버에 요청할때, create 인지 update인지 고민하였다.
camera와 analyze image는 연관되어 있지만 camera라는 리소스 자체가 analyze image는 아니기 때문에(is가 아님) create 한 다음에 camera와 연관지어주면 된다(has 이기 때문에).
- nginx, gunicorn
   - WSGI 자료 : https://sgc109.github.io/2020/08/15/python-wsgi/
   - gunicorn(WSGI Server) 사용 방법
     1. pip install gunicorn
     2. wsgi.py 생성.
        from app import app
        main 메서드 추가
     3. gunicorn --bind 0.0.0.0:5000 wsgi:app
     4. linux에서는 systemd를 통해 자동으로 서버가 자동으로 구동되도록 설정하여 사용한다.
- server framework
  - fast api
  - node.js
