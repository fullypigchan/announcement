# 담당 업무 소개

  무역 및 비즈니스 네트워킹 플랫폼 **GlobalGates** 프로젝트에서 제가 맡은 기능들을 소개합니다.

  <br>

  ## 🔖 북마크 (Bookmark)

  REST API를 활용해 사용자가 북마크한 게시물들을 메인 페이지에 불러옵니다.
  별도의 분류 없이 북마크할 경우 **미분류 북마크**로 자동 저장되며, 사용자가 새로운 북마크 폴더를
   생성한 뒤 해당 폴더를 선택하면 게시물이 지정된 폴더로 분류되어 저장됩니다.

  **핵심 기술**
  - **REST API** 기반 게시물 조회 — 폴더/미분류 구분 없이 일관된 인터페이스로 불러오기
  - **자동 분류 로직** — 분류를 지정하지 않으면 자동으로 *미분류* 폴더에 fallback 저장되어 데이터
   유실 방지
  - **즉시 재분류** — 사용자가 폴더를 생성하면 기존 미분류 항목을 손쉽게 폴더로 이동

  **주요 특징**
  - REST API 기반 게시물 불러오기
  - 미분류 / 사용자 정의 폴더로 자동 분류
  - 메인 페이지에서 한눈에 확인 가능

  <p align="center">
    <img src="./images/bookmark.png" alt="북마크 API Swagger UI" width="700">
  </p>

  <br>

  ## 📰 뉴스 (News)

  **탐색하기** 페이지의 뉴스 탭과 페이지 하단 **푸터의 뉴스 영역**에서 최신 뉴스를 노출합니다.
  뉴스 항목을 클릭하면 뉴스 상세 페이지로 이동하며, 일반 뉴스 콘텐츠가 표시됩니다.

  **핵심 기술**
  - **공용 컴포넌트 재사용** — 동일한 뉴스 데이터를 탐색/푸터 두 곳에 사용하지만 컴포넌트는 한
  번만 작성
  - **REST API + 상세 라우팅** — 목록 → 상세로 자연스러운 페이지 이동, 단일 진입점으로 일관성
  유지

  **주요 특징**
  - 탐색하기 페이지 + 푸터 영역에 동시 노출
  - 클릭 시 뉴스 상세 페이지로 이동
  - 무역 관련 일반 뉴스 제공

  <p align="center">
    <img src="./images/news.png" alt="뉴스 API Swagger UI" width="700">
  </p>

  <br>

  ## 👥 커뮤니티 (Community)

  무역 사업자들이 자신의 관심 품목이나 카테고리별로 **커뮤니티를 직접 생성**할 수 있습니다.
  사용자들은 해당 커뮤니티 내에서 게시물을 작성하고, 대화를 나누며, 무역 관련 정보를 자유롭게
  공유할 수 있습니다.

  **핵심 기술**
  - **카테고리 ↔ 멤버 M:N 관계 설계** — 한 사업자가 *수출*, *IT*, *반도체* 처럼 여러 카테고리에
  동시에 속할 수 있어 다중 필터링 검색이 자연스럽게 동작
  - **카테고리 트리 구조** — 대분류(수출/수입/물류 …) 아래 세부 카테고리(미주/유럽/동남아 …)를
  두는 **부모-자식 계층 구조** 로 관심사를 좁혀 들어갈 수 있음

  **주요 특징**
  - 관심 품목 · 카테고리별 커뮤니티 생성
  - 게시물 작성을 통한 정보 공유
  - 사업자 간 자유로운 소통 환경 제공

  <p align="center">
    <img src="./images/community.png" alt="커뮤니티 API Swagger UI" width="700">
  </p>

  <br>

  ## 💬 채팅 (Chat)

  전문가와 개인 사업자 간의 소통을 매개하는 채널로, **메일의 무거운 접근성을 해소**하고
  커뮤니티형 플랫폼의 성격에 맞춰 실시간 채팅 방식을 채택했습니다.
  채팅 내에서 사진 업로드 및 다운로드가 모두 가능하며, **AWS S3**를 활용하여 클라우드에 파일을
  저장하고 불러오는 방식으로 파일을 관리합니다.

  **주요 특징**
  - 전문가 ↔ 개인 사업자 간 실시간 소통
  - 메일 대비 가벼운 접근성 제공
  - AWS S3 기반 사진 업로드 / 다운로드
  - 클라우드 파일 관리

  ### 🐇 왜 RabbitMQ를 사용했나요?

  실시간 채팅에서 가장 중요한 것은 **"보낸 메시지가 받는 사람에게 정확하고 안정적으로 도착하는 
  것"** 입니다.
  이를 위해 메시지를 직접 주고받게 두지 않고, 그 사이에 **메시지 브로커(message broker)** 를 두어
   중계합니다.
  프로젝트에서는 가장 널리 쓰이는 오픈소스 브로커인 **RabbitMQ** 를 채택했습니다.

  > "RabbitMQ is a powerful, enterprise grade open source messaging and streaming broker."
  > — RabbitMQ 공식 홈페이지 ([rabbitmq.com](https://www.rabbitmq.com/))

  > "Messaging brokers receive messages from publishers (applications that publish them, also
  known as producers) and route them to consumers (applications that process them)."
  > — RabbitMQ 공식 튜토리얼 ([AMQP 0-9-1 Model 
  Explained](https://www.rabbitmq.com/tutorials/amqp-concepts))

  쉽게 말해 RabbitMQ는 **채팅 메시지를 받아 잠시 보관했다가, 받을 사람에게 정확히 배달해 주는 
  "우체국"** 같은 역할을 합니다.
  공식 문서 역시 이 구조를 우체국에 비유하여 설명합니다.

  > "Messages are published to exchanges, which are often compared to post offices or mailboxes.
  Exchanges then distribute message copies to queues using rules called bindings."
  > — RabbitMQ 공식 튜토리얼 ([AMQP 0-9-1 Model 
  Explained](https://www.rabbitmq.com/tutorials/amqp-concepts))

  **도입으로 얻은 이점**
  - **안정적인 전달** — 서버가 잠시 바빠도 메시지는 큐에 쌓였다가 차례로 처리되므로 누락 위험이
  낮음
  - **확장성** — 서버를 여러 대로 늘려도 브로커가 메시지를 중앙에서 분배하여, 모든 서버의
  사용자에게 동일하게 전달
  - **역할 분리** — 보내는 쪽과 받는 쪽이 서로를 직접 알 필요 없이, 브로커만 보고 통신할 수 있어
  시스템 결합도가 낮음

  ### 📦 그 외 채팅에 적용된 기술

  - **WebSocket(STOMP) 실시간 양방향 통신** — 메시지가 들어오는 즉시 화면에 반영
  - **DB 영속화 + AFTER_COMMIT 전파** — 데이터베이스에 저장이 끝난 메시지만 상대방에게 전송하여, 
  *새로고침해도 사라지지 않는 채팅* 보장
  - **AWS S3 클라우드 스토리지** — 첨부 이미지를 자체 서버가 아닌 S3에 저장해 부하 분산과 
  안정적인 다운로드 제공

  <p align="center">
    <img src="./images/chat.png" alt="채팅 API Swagger UI" width="700">
  </p>

  <br>
