```diff
- 해당 API는 테스트 버전 입니다. Production 버전에서 이용하지 마십시오.
- 해당 API는 테스트 단계이므로 API서버에 접속이 원활하지 않을 수 있습니다.
```

## 소개

`FiveM 리얼월드 2022` 공개 API 입니다. 해당 API를 이용하여 리얼월드 2022 의 게임 데이터에 빠르게 접근하고 인게임에서 제공하는 서비스를 편리하게 이용할 수 있습니다.<br>
- [lua-sdk](https://github.com/fivem-realw/RW-API/tree/main/lua)
- [node-sdk](https://github.com/fivem-realw/RW-API/tree/main/node)
<br><br>

## API 엔드포인트

```
https://api.realw.kr/game/v1
```

### 사용자 인증
API 호출시 리얼월드로 부터 발급받은 `API Key` 를 `X-API-Credential` 헤더로 전송해야 합니다.<br>
해당 헤더가 존재하지 않거나 올바르지 않은 `API Key` 가 전송되면 API 호출이 서버 대기열에서 삭제됩니다.

### 요청 빈도 제한
API 호출은 IP별 분당 100회로 제한됩니다. 더 많은 빈도 제한을 원하면 discord.gg/realw 로 문의 바랍니다.

### HTTP 반환 코드
- HTTP 4XX 반환 코드는 잘못된 요청에 사용됩니다. 문제는 호출자 측에 있습니다.
- HTTP 403 반환 코드는 WAF 제한(웹 응용 프로그램 방화벽)을 위반했을 때 사용됩니다.
- HTTP 429 반환 코드는 요청 속도 제한을 위반할 때 사용됩니다.
- HTTP 418 반환 코드는 코드를 받은 후 요청을 계속 보내기 위해 IP가 자동 금지되었을 때 사용됩니다.
- HTTP 5XX 반환 코드는 내부 오류에 사용됩니다. 문제는 API 서버측입니다.
<br><br>

## API 목록

- 모든 API 호출에는 X-API-Credential 헤더가 포함되어야 합니다.

### 서버

**서버 연결정보**
> 서버의 접속가능한 연결정보를 표시합니다.
```
GET /server/connectInfo
```
**서버 상태**
> 서버의 Online/Offline 여부 및 접속가능 여부를 표시합니다.
```
GET /server/status
```
**서버 리소스 정보**
> 서버의 리소스정보, 맵정보 및 컨텐츠 정보를 표시합니다.
```
GET /server/resourceInfo
```
**접속자 목록**
> 현재 서버의 접속된 유저정보를 출력합니다. 
```
GET /server/getUserList
```
<hr>

### 고유번호
**마지막 배정 고유번호**
> 마지막으로 배정된 고유번호를 출력합니다.
```
GET /uid/latest
```
**현재 고유번호 배정범위**
> 현재 배정되는 고유번호의 범위를 출력합니다.
```
GET /uid/getCurrentRange
```
**다음 고유번호 배정범위**
> 다음 배정되는 고유번호의 범위를 출력합니다.
```
GET /uid/getNextRange
```
<hr>

### 아이템

**아이템 목록**
> 모든 아이템 목록 및 정보를 출력합니다.
```
GET /item/getList
```
- 매개변수
<table>
  <thead>
    <tr>
      <td>매개변수 명</td>
      <td>매개변수 타입</td>
      <td>필수값</td>
      <td>설명</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>type</td>
      <td>INT</td>
      <td>아니요</td>
      <td></td>
    </tr>
    <tr>
      <td>limit</td>
      <td>INT</td>
      <td>아니요</td>
      <td></td>
    </tr>
  </tbody>
</table>

**아이템 정보 조회**
> 아이템 정보를 조회합니다.
```
GET /item/getInfo
```
<hr>

### 계정

**계정 ID**
> 유저ID로 부터 식별자를 가져옵니다.
```
GET /account/getIdentifierByUserId
```
- 매개변수
<table>
  <thead>
    <tr>
      <td>매개변수 명</td>
      <td>매개변수 타입</td>
      <td>필수값</td>
      <td>설명</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>id</td>
      <td>STRING</td>
      <td>예</td>
      <td></td>
    </tr>
  </tbody>
</table>
<hr>

### 유저

**유저 정보**
> 유저 정보를 출력합니다.
```
GET /user/getUserInfo
```

**유저 아이템 목록**
> 유저의 아이템 목록을 조회합니다.
```
GET /user/getItemList
```
**아이템 주기**
> 다른 유저의 계정으로 아이템을 이동합니다.
```
POST /user/giveItem
```
<hr>

### 랭크

**플레이 타임 순위**
> 유저의 누적 플레이 타임 순위를 표시합니다.
```
GET /rank/playTime
```
<hr>

### 채팅
**채팅 목록**
> 채팅 목록을 조회합니다.
```
GET /chat/latest
```
**채팅 보내기**
> 채팅을 보냅니다.
```
POST /chat/sendMessage
```
<hr>

### 권한
**권한 목록**
> 권한 목록을 조회합니다.
```
GET /permission/getList
```
**권한 주기**
> 유저에게 권한을 추가합니다.
```
POST /permission/addUser
```
**권한 삭제**
> 유저로부터 권한을 제거합니다.
```
POST /permission/removeUser
```
<hr>