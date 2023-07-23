# pharmacy_Find
Docker 란 ?
- 컨테이너를 사용하여 응용프로그램을 더 쉽게 만들고 배포하고 실행할 수 있도록 설계된 도구이며 컨테이너
  기반의 오픈소스 가상화 플랫폼
- 일반 컨테이너 개념에서 물거을 손쉽게 운송해주는 것처럼 어플리케이션 환경에 구애 받지 않고 손쉽게
  배포 관리를 할 수 있게 해준다.
- 컨테이너 기반 배포 방식은 구글을 비롯해 대부분 서비스 회사가 컨테이너로 서비스 운영
- 따라서 AWS, Azure, Google Cloud등 어디서든 실행이 가능
<br>
<br>
<hr>
Docker를 왜 굳이 사용해야 할까 ?<br>
- 똑같은 일을 하는 2대의 서버가 있다 해도, A 서버는 1년전에 구성했고 B서버는 이제막 구성헀다면 운영체제부터 컴파일러,
  설치된 패키지까지 완벽하게 같기는 쉽지 않다.<br>
- 이러한 차이가 문제를 발생시킬 수 있다.<br>
- A서버는 되는데 B서버는 왜 안되지?<br>
- Docker는 서버마다 동일한 환경을 구성해주기 때문에 이러한 문제를 해결할 수 있다.<br>
- 동일한 환경을 구성하기 때문에 auto scaling에 유리 하다.<br>
- 한대의 서버에서 하나의 어플리케이션만 운영하는 전통적인 방식에서 하이퍼바이저 기반 가상화 등장<br>
- 하이퍼 바이저는 호스트 시스템(윈도우, 리눅스 등)에서 다수의 게스트 OS(가상머신)을 <br>
  구동할 수 있게 하는 소프트 웨어<br>
- 각 VM마다 독립적으로 동작<br>
- 도커는 하이퍼 바이저 구조를 토대로 등장했으며, VM보다 훨신 가볍게 동작하기 때문에 성능에 유리<br>
<br>
<br>
<hr>
Docker의 컨테이너와 이미지<br>
- 이미지란 코드, 런타임, 시스템 도구, 시스템 라이브러리 및 설정과 같은<br>
  응용프로그램을 실행 하는데 필요한 모든 것을 포함하는 패키지<br>
- 이미지 Github와 유사한 서비스인 https://hub.docker.com/ 을 통해 버전 관리 <br>
- 컨테이너란 도커 이미지를 독립된 공간에서 실행할 수 있게 해주는 기술<br>
- 프로그램을 실행하는데 필요한 종속성들을 가지고 있다.<br>
- 이미지 인스턴스이며 설정이나 프로그램을 실행한다.<br>
<br>
<br>
<hr>
Docker 파일 이란?<br>
- Dockerfile이란 도커 이미지를 구성하기 위해 있어야할 패키지, 의존성, <br>
  소스코드 등을 하나의 file 기록하여 이미지화 시킬 명령 파일<br>
- 즉, 이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 더 이상 새로운 <br>
  서버가 추가되면 의존성 파일을 컴파일하고 이것 저것 설치할 필요가 없다.<br>
<br>
<br>
<hr>
Dockerfile 주요 명령어<br>
- FROM : // 새로운 이미를 생성할때 기반으로 사용할 이미지를 지정(이미지 이름:태그)<br>
         // jdk11이 있는 컨테이너 사용<br>
         FROM openjdk11 <br>
- ARG : // 이미지 빌드 시점에서 사용할 변수 지정 <br>
        ARG JAR_FILE=build/lib/app.jar <br>
- COPY : // 호스트에 있는 파일이나 디렉토리를 Docker 이미지의 파일 시스템으로 복사 <br>
          COPY${JAR_FILE}./app,jar <br>
- ENV : // 컨테이에서 사용할 환경 변수 지정 <br>
        // TimeZone환경 변수 <br>
        ENV TZ=Asia/Seoul <br>
- ENTRYPOINT : // 컨테이너가 실행되었을 때 항상 실행되어야 하는 커맨드 지정 <br>
              ENTRYPOINT["java","-jar","./app.jar"] <br>
<br>
<br>
<hr>
Docker Compose란? <br>
- Docker Compose란 멀티 컨테이너 도커 어플리케이션을 정의하고 실행하는 도구 <br>
- Application, Database, Redis, Nginx등 각 독립적인 컨테이너로 관리한다고 했을 때 다중 컨테이너 라이프 사이클을 어떻게 <br>
  관리해야 할까? <br>
- 여러개의 도커 컨테이너로 부터 이루어진 서비스를 구축 및 네트워크 연결, 실행 순서를 자동으로 관리 <br>
- docker-compose.yml 파일을 작성하여 1회 실행하는 것으로 설정된 모든 컨테이너를 실 <br>




  
