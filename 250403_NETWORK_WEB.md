# **✅ 1. HTTP 프로토콜**

## **❓기본 질문: HTTP란 무엇인가요?**

HTTP(HyperText Transfer Protocol)는 웹 상에서 클라이언트와 서버가 데이터를 주고받기 위한 **비연결성(Connectionless)**, **무상태성(Stateless)** 기반의 **애플리케이션 계층** 프로토콜입니다.

### **1-1. HTTP는 왜 무상태성인가요?**

<aside>
💡

“요청 하나하나가 서로 독립적”

</aside>

- HTTP는 각 요청이 서로 독립적으로 동작하며, 서버는 이전 요청의 상태를 기억하지 않기 때문입니다. 따라서 확장성이 높지만, 사용자 인증 등 상태 유지가 필요한 경우에는 쿠키나 세션이 필요합니다.

### **1-2. HTTP 1.1과 HTTP 2.0의 차이점은?**

<aside>
💡

“한 연결에서 여러 개를 동시에 처리할 수 있다면?”

</aside>

- HTTP 2.0은 다중화(Multiplexing), 헤더 압축, 서버 푸시 기능을 통해 HTTP 1.1의 성능 문제를 개선했습니다. 특히 하나의 TCP 연결에서 여러 요청/응답을 병렬로 처리할 수 있어 성능이 향상됩니다.

### **1-3. HTTP 메서드(GET, POST, PUT, DELETE) 차이는?**

- GET: 리소스 조회 (캐싱 가능, 본문 없음)
- POST: 리소스 생성 (본문 있음, 캐싱 안됨)
- PUT: 리소스 전체 수정
- DELETE: 리소스 삭제

# **✅ 2. HTTP vs HTTPS**

## **❓기본 질문: HTTP와 HTTPS의 차이점은?**

HTTPS는 HTTP에 **SSL/TLS 암호화 계층**이 추가된 프로토콜입니다. HTTPS는 데이터의 기밀성(암호화), 무결성(위조 방지), 인증성(서버 신원 보장)을 제공합니다.

### **2-1. SSL/TLS의 역할은 무엇인가요?**

SSL/TLS는 통신 데이터를 암호화하여 도청과 중간자 공격을 방지합니다.

또한 **서버 인증서 검증**, **대칭키 교환**, **메시지 무결성 검증** 등의 보안 기능을 제공합니다.

### **2-2. HTTPS는 어떻게 보안을 보장하나요?**

<aside>
💡

“공개키를 어디서 주고, 대칭키는 누가 만들죠?”

</aside>

1.	서버는 인증서를 통해 공개키를 전달합니다.

2.	클라이언트는 이 공개키로 대칭키를 암호화해 전달합니다.

3.	이후엔 **대칭키**를 통해 양방향 데이터를 암호화해 통신합니다.

“**공개키는 대칭키 전달용**, **대칭키는 실제 데이터 암호화용**”

### **2-3. HTTPS에서 사용되는 암호화 방식은 어떤 것이 있나요?**

HTTPS는 **하이브리드 암호화 방식**을 사용합니다:

- **공개키 암호화(RSA, ECDHE)**: 대칭키를 안전하게 교환
- **대칭키 암호화(AES, ChaCha20)**: 실제 데이터 암호화 (빠르고 효율적)
- **해시 알고리즘(SHA-256)**: 메시지 무결성 검증 (HMAC 등)

심화) 최신 TLS에서는 **ECDHE(Elliptic Curve Diffie-Hellman Ephemeral)** 방식으로 Perfect Forward Secrecy(PFS)도 보장합니다.

### **2-4. 인증서는 무엇이고 왜 필요한가요?**

인증서는 서버의 공개키가 신뢰할 수 있는 기관(CA)에 의해 검증되었다는 것을 보장하는 디지털 문서입니다.

브라우저는 CA 목록을 통해 서버 인증서가 유효한지를 판단합니다.

# **✅ 3. TCP 3-way handshake**

## **❓기본 질문: TCP 연결은 어떻게 성립되나요?**

1. 클라이언트 → 서버 : SYN
2. 서버 → 클라이언트 : SYN-ACK
3. 클라이언트 → 서버 : ACK

이 과정을 통해 **신뢰성 있는 연결**을 수립합니다.

### **3-1. TCP 연결 종료는 어떻게 되나요?**

- 종료는 4-way handshake로 진행되며, 이 과정은 데이터 손실 없이 연결을 종료하기 위함입니다.
1. FIN  (클라이언트 → 서버) : 클라이언트 전송 종료 요청 (연결 닫을게요)
2. ACK → (클라이언트 ← 서버) : 서버 확인 응답 (알았어요)
3. FIN → (클라이언트 ← 서버) : 서버도 전송 종료 요청 (나도 닫을게요)
4. ACK → (클라이언트 → 서버) : 클라이언트 확인 응답 (확인했어요)

https://github.com/GOORM-DEEPDIVE-first-study/CS-/issues/6

### **3-2. TCP는 OSI 7계층 중 어디에 해당하나요?**

- TCP는 **전송 계층(4계층)** 프로토콜입니다. 신뢰성, 흐름 제어, 혼잡 제어 등의 기능을 수행합니다.

# **✅ 4. REST API**

## **❓기본 질문: REST API란 무엇이고, 왜 사용하나요?**

REST는 자원을 URI로 표현하고, HTTP 메서드로 조작하는 아키텍처 스타일입니다. **무상태성**, **일관된 인터페이스**, **계층화된 시스템** 등의 제약 조건을 따르며, API 설계의 표준으로 많이 사용됩니다.

### **4-1. REST의 장점은 무엇인가요?**

- 무상태성 → 서버 확장성 향상
- server - client 구조
- 간결하고 직관적
- URI로 자원 식별 → 명확한 API 구조
- 캐시 가능 → 성능 향상

### **4-2. RESTful하지 않은 API 예시는?**

- POST /getUserData → 동작이 URL에 포함됨
- URI는 자원 표현이어야 하며, 동사는 HTTP 메서드로 표현해야 함.

# **✅ 5. CORS**

## **❓기본 질문: CORS란 무엇인가요?**

브라우저의 **보안 정책(Same-Origin Policy)**으로 인해, 다른 출처(origin)의 리소스에 접근할 수 없습니다. 이를 우회하기 위해 **CORS(Cross-Origin Resource Sharing)**가 사용됩니다.

### 같은 출처의 범위가 어떻게 될까요?

같은 출처(Same-Origin)는 `Protocol + Hostname + Port` 세 가지 요소가 모두 동일한 경우를 말합니다.

이 중 **하나라도 다르면 다른 출처(Cross-Origin)**간주되며, 브라우저의 보안 정책(Same-Origin Policy)에 따라 **교차 출처 요청은 제한**됩니다.

### **5-1. 브라우저에서 CORS가 필요한 이유는?**

브라우저는 **Same-Origin Policy**라는 보안 정책을 적용합니다. 이는 악의적인 웹사이트에서 사용자의 권한(쿠키, 토큰 등)을 이용해 다른 도메인에 임의로 요청을 보내는 것을 **방지하기 위한 보호 장치**입니다.

하지만 실제 서비스에서는 프론트엔드와 백엔드가 **다른 도메인/포트**에 존재하는 경우가 많기 때문에, 이런 합법적인 요청을 허용하기 위한 방법이 바로 **CORS**입니다.

### **5-2. CORS 요청에서 단순 요청이 아닌 경우 Preflight 요청 보내기도 하는데요, Preflight 요청이 무엇인지, 단순 요청이 아닌 상황에는 어떠한 것들이 있는지 설명해주세요.**

- Preflight는 실제 요청 전에 `OPTIONS` 메서드로 서버에 허용 여부를 묻는 사전 요청입니다. PUT, DELETE, Content-Type이 application/json인 경우 등에서 발생합니다.
- CORS 정책에서 브라우저는 **보안상의 이유로** 출처가 다른 도메인에 HTTP 요청을 보낼 때, 요청이 **안전한지 미리 확인하는 절차**를 거치기도 합니다. 이걸 **Preflight 요청**이라고 하며, 실제 요청 전에 **OPTIONS 메서드**로 서버에 문의합니다.

1. **HTTP 메서드가 다음에 해당하지 않을 경우**: `GET`, `POST` , `HEAD`
2. **Content-Type이 아래에 포함되지 않을 경우**
    1. content type이 `application/x-www-form-urlencoded` , `multipart/form-data`  , `text/plain`  가 아닐 때
3. **커스텀 헤더가 포함된 경우 →** `Authorization`, `X-Custom-Header`
4. **Credential** 설정이 있을 때 → `withCredentials: true`

### 5-3. Preflight는 네트워크 지연과 성능 저하가 발생합니다. 이를 어떻게 해결할 수 있을까요?

1. **Preflight 캐싱을 적극적으로 사용**
서버 응답에 다음과 같은 헤더 추가 → 브라우저는 Preflight 요청 결과를 3600초(1시간) 동안 캐시하므로 같은 요청에 대해 재요청하지 않음
    
    ```jsx
    Access-Control-Max-Age: 3600
    ```
    
2. 프론트엔드 → 백엔드 도메인을 **같은 origin**으로 통합
    
    ex) reverse proxy(Nginx 등) 사용
    

### **5-4. CORS를 해결하는 방식으로 어떠한 것이 있을까요? 서버에서 CORS를 허용하려면?**

- 응답 헤더에 설정

```bash
Access-Control-Allow-Origin: http://example.com
Access-Control-Allow-Methods: GET, POST
```

# **✅ 6. 쿠키, 세션, JWT 인증**

## **쿠키 / 세션 / 토큰 기반 인증 방식의 차이**

### **❓인증 상태를 유지하기 위한 방식에는 어떤 것이 있고, 각각 어떤 특징이 있나요?**

HTTP는 **무상태(stateless)**이기 때문에, 사용자가 로그인한 뒤에도 상태를 유지하려면 별도의 인증 방식이 필요합니다. 대표적으로 세 가지가 있습니다.

| **방식** | **저장 위치** | **동작 원리** | **장점** | **단점** |
| --- | --- | --- | --- | --- |
| **쿠키** | 클라이언트 (브라우저) | key-value 저장, 자동 요청 | 간단, 클라이언트 주도 | 보안 위험(XSS, 탈취) |
| **세션** | 서버 | 세션 ID를 쿠키로 전달, 서버는 상태 보관 | 구현 쉽고 제어 용이 | 확장성 낮음 (메모리 사용) |
| **JWT** | 클라이언트 | 서명된 토큰 발급 → 헤더로 요청 | 무상태, 확장성 우수 | 탈취 시 만료까지 취약 |

### **그럼 각각은 언제 적합한가요?**

**❓세션 기반과 토큰(JWT) 기반 인증 방식은 각각 어떤 상황에 적합한가요?**

**답변**:

| 전통적인 웹사이트 (모놀리식 서버) | 세션 기반 |
| --- | --- |
| MSA, SPA, 모바일 앱, API 서버 | JWT (토큰 기반) |
| 높은 보안 통제 필요 | 세션 (서버가 직접 만료 처리 등 제어) |
| 대규모 트래픽, 무상태 서버 구성 필요 | JWT (분산 환경에 적합) |

### **그럼 JWT가 자주 쓰이는데, 어떻게 동작하나요?**

**❓JWT는 무엇이고 어떻게 인증에 사용되나요?**

JWT(JSON Web Token)는 서버가 로그인된 사용자에게 발급하는 **서명된 토큰**입니다. 이 토큰은 **사용자 정보와 서명(Signature)**을 포함하며, 클라이언트는 이후 요청에 이 토큰을 **Authorization 헤더에 포함**해서 보냅니다.

서버는 이 토큰을 검증함으로써 사용자를 인증할 수 있습니다.

- **장점**: 서버가 상태를 저장하지 않아도 되므로, 무상태(stateless) 서버 구성 가능
- **주의점**: 토큰이 탈취되면 만료 전까지 악용 가능 → 만료 시간, 재발급 전략 필요

**❓ JWT의 구조는 어떻게 되나요?**

JWT는 3부분으로 구성됩니다:

헤더(Header).페이로드(Payload).서명(Signature)

각각 Base64로 인코딩되어 .으로 구분됩니다.

- **Header**: alg(서명 알고리즘), typ(JWT)
- **Payload**: 사용자 정보, 만료 시간 등
- **Signature**: 서버 비밀키로 Header+Payload를 서명한 값

**❓JWT는 서버가 저장하지 않는데, 어떻게 인증 상태를 유지하나요?**

JWT 자체에 인증 정보가 포함되어 있고, **서명으로 위조 여부 검증**이 가능하기 때문에 **서버가 별도로 상태를 저장하지 않아도** 인증이 가능합니다.

**❓JWT 토큰이 탈취되면 어떻게 되나요?**

JWT는 기본적으로 만료 시간까지 유효하므로, **탈취되면 만료 전까지 계속 사용할 수 있습니다.**

그래서 몇가지 보완이 필요합니다

- HTTPS로 전송
- 토큰 만료 시간 짧게 설정 + Refresh Token 전략 사용
- 토큰 블랙리스트 (로그아웃 등 시 무효화)

**❓JWT와 세션을 함께 쓰는 경우도 있나요?**

네. 예를 들어, **Access Token은 JWT**, **Refresh Token은 서버 세션에 저장**해서 토큰 재발급 시 검증하는 하이브리드 방식도 많이 사용됩니다.

# **✅ 7. 로드 밸런싱**

## **❓기본 질문: 로드 밸런싱이란?**

여러 서버에 요청을 **균등하게 분산**시켜 가용성과 성능을 향상시키는 기술입니다. 주로 **L4 (TCP/IP)** 또는 **L7 (HTTP)** 레벨에서 작동합니다.

**🔁 꼬리 질문**•	

### **7-1. 로드 밸런싱 알고리즘의 종류는?**

- 정적: Round Robin, IP Hash
- 동적: Least Connections(최소 연결), Least Response Time(최소 응답 시간) 기반, Weighted Least Connection(가중치 최소 연결 방식) 등

### **7-2. MSA에서 로드 밸런싱 시 주의할 점은?**

- 서비스 디스커버리와 통합 필요
- 서비스 간 통신 → 로드 밸런서로 인한 지연 또는 병목 가능성
- Circuit Breaker, Retry 전략 필요

### **7-3. 클라이언트 사이드 vs 서버 사이드 로드 밸런싱?**

- 클라이언트 사이드: 클라이언트가 인스턴스를 선택 (ex. Ribbon, gRPC)
- 서버 사이드: 중앙 로드 밸런서가 분산 (ex. Nginx, ELB)

# **✅ 8. OSI 7계층**

## **❓기본 질문: OSI 7계층이란?**

네트워크 통신을 7개의 계층으로 나눈 모델로, 각 계층이 특정 역할을 담당하여 **모듈화, 호환성, 표준화**를 가능하게 합니다.

![image](https://github.com/user-attachments/assets/83e2f72f-9a80-473d-89bd-38d187f1fe2a)


### **8-1. 각 계층의 역할은?**

1. 물리: 데이터를 전기 신호로 바꾸어주는 계층 (`bit` 단위)
전기/신호 전송
2. 데이터 링크: 데이터의 물리적인 전송과 에러 검출, 흐름 제어, `MAC` 주소를 통한 통신 (`Frame` 단위)
ex) 이더넷
3. 네트워크: 패킷을 목적지까지 가장 빠른 길로 전송하기 위한 계층(`Packet` 단위)
IP, Router 
4. 전송: 최송 수신 프로세스로 데이터의 전송 담당(`Segment` 단위), 
ex) TCP/UDP
5. 세션: TCP/IP 세션 연결 유지/관리
6. 표현: 데이터 형식(Format) 정의, 인코딩, 암호화
7. 응용: HTTP, FTP 등 사용자에게 통신을 위한 서비스 제공, 인터페이스

### **8-2. HTTP는 몇 계층 인지?**

7계층(응용 계층)에 속합니다.

### **8-3. TCP와 IP는 각각 어디?**

- TCP: 4계층(전송 계층)
- IP: 3계층(네트워크 계층)
