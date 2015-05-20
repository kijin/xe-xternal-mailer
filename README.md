
외부 서버 & API 메일 발송 애드온
================================

Gmail 등의 외부 SMTP 서버, 우리메일 API, 그리고 Amazon SES, Mailgun, Mandrill, Sendgrid 등
세계적인 메일 발송 전문업체들의 API를 사용하여 메일을 발송하도록 해주는 애드온입니다.
XE에 내장된 `Mail` 클래스를 대체하므로
회원가입 인증메일 발송, ID/비밀번호 찾기 등
`Mail` 클래스에 의존하는 기존의 모든 코드를 그대로 사용할 수 있습니다.

외부 SMTP 서버나 메일 발송 전문업체의 API를 사용하면
일반적인 웹호스팅 서버에서 직접 메일을 발송하는 것보다 훨씬 안정적으로 메일이 전달되고,
업체에서 안내하는 대로 도메인에 SPF, DKIM 등을 적용하면 스팸 필터에 걸릴 확률도 크게 줄어듭니다.
가입인증을 비롯한 중요한 메일이 잘 도착하지 않아 어려움을 겪으셨다면
이 애드온을 사용해 보세요.

XE 1.8 이상, PHP 5.3 이상에서 사용 가능합니다.

**[주의]** 인증 및 알림 용도로 소량의 메일을 자주 발송하기에 적합한 애드온입니다.
전체공지나 광고 등 대량메일을 발송할 때는 전문업체를 직접 이용하시기 바랍니다.

설치 방법
---------

이 애드온을 사용하려면 XE의 `config/config.inc.php`에서 아래의 한 줄을 찾아

    require(_XE_PATH_ . 'classes/mail/Mail.class.php');

아래와 같이 주석처리해 주어야 합니다.

    //require(_XE_PATH_ . 'classes/mail/Mail.class.php');

XE에 내장된 `Mail` 클래스가 먼저 로딩될 경우 이 애드온이 동작하지 않기 때문입니다.

설정하기
--------

### PHP mail() 함수

서버 자체의 메일 발송 기능을 사용합니다. XE에 내장된 `Mail` 클래스와 큰 차이가 없습니다.

### 외부 SMTP 서버

Gmail을 비롯하여 SMTP를 지원하는 메일 계정이라면 모두 사용할 수 있습니다.

  - 발송 방법: 외부 SMTP 서버
  - SMTP 서버: 서버명 (예: `smtp.gmail.com`)
  - SMTP 포트: 465, 587 또는 25
  - SMTP 보안: 465번 포트인 경우 `SSL`, 587번 포트인 경우 `TLS`, 25번 포트인 경우 사용하지 않음
  - 아이디: 메일 계정 아이디
  - 암호 또는 API 키: 메일 계정 비밀번호

### Amazon SES API

클라우드 서비스로 유명한 아마존에서 운영하는 메일 발송 서비스입니다.
메일 1건당 가격이 매우 저렴하다는 장점이 있으나, 처음 셋팅하는 과정이 다소 복잡하고
일부 포털에는 배달이 되지 않거나 스팸으로 취급받기도 하니 주의하시기 바랍니다.

  - 발송 방법: Amazon SES API
  - SMTP 서버: AWS Endpoint (예: `us-east-1`)
  - SMTP 포트, 보안: 비워두어도 됨
  - 아이디: AWS Access Key
  - 암호 또는 API 키: AWS Secret Key

### Mailgun API

대형 IDC 업체인 Rackspace에서 운영하는 API입니다.
셋팅은 비교적 간단하고, 월 10,000건까지 무료로 발송할 수 있습니다.
설정할 때 반드시 도메인을 입력해야 하니 주의하세요.

  - 발송 방법: Mailgun API
  - SMTP 서버, 포트, 보안: 비워두어도 됨
  - 아이디: 도메인 입력
  - 암호 또는 API 키: API key 입력

### Mandrill API

대량메일 발송 전문업체인 Mailchimp에서 트랜잭션 메일 발송을 위해 별도로 개발한 상품입니다.
셋팅이 매우 간단하고, 월 12,000건까지 무료로 발송할 수 있습니다.

  - 발송 방법: Mandrill API
  - SMTP 서버, 포트, 보안: 비워두어도 됨
  - 아이디: 비워두어도 됨
  - 암호 또는 API 키: API key 입력

### Postmark API

트랜잭션 메일 발송 전문업체로, 대량메일은 취급하지 않습니다.
셋팅이 매우 간단하고, 최초 가입시 25,000건을 발송할 수 있는 포인트가 적립됩니다.

  - 발송 방법: Postmark API
  - SMTP 서버, 포트, 보안: 비워두어도 됨
  - 아이디: 비워두어도 됨
  - 암호 또는 API 키: API key 입력

### Sendgrid API

대량메일 발송 전문업체이며, 월 회비가 있지만 하루 400건(월 12,000건)까지는
무료로 사용할 수 있습니다. 셋팅은 비교적 간단합니다.

  - 발송 방법: Sendgrid API
  - SMTP 서버, 포트, 보안: 비워두어도 됨
  - 아이디: Sendgrid 회원 아이디
  - 암호 또는 API 키: Sendgrid 회원 비밀번호

### 우리메일 API

XE 기반으로 운영되는 국내 대량메일 발송 전문업체입니다.
월 10,000건까지 무료로 사용할 수 있습니다.
현재는 보낸이의 메일주소를 직접 지정하거나 파일을 첨부할 수 없으니 유의하세요.

  - 발송 방법: Woorimail API
  - SMTP 서버, 포트, 보안: 비워두어도 됨
  - 아이디: 인증키 발급시 입력한 도메인
  - 암호 또는 API 키: 인증키
