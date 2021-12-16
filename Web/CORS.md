# CORS

### **CORS는**

- Same-Origin의 반대 말로, Cross-Origin Resource, 교차 출차 자원 공유 방식이라고 부릅니다.
- 웹 어플리케이션이 다른 origin의 리소스에 접근, 공유할 수 있도록 하는 매커니즘을 말합니다.

### **사용 목적은**

다른 origin에서 나의 리소스에 함부로 접근하지 못하게 하기 위해 사용합니다. 즉, 허용한 origin들만 요청할 수 있도록 하기 위해 필요합니다.

### **NodeJS 기반의 웹 서버에서 CORS 설정 방법은**

- Access-Control-Allow-Origin로 접근 범주를 설정합니다. 모두가 가능하게 하려면 * (와일드키)를 사용할 수 있으며,
- 토큰이나 사용자 식별 정보다 담겨져 있으며 보내는 측에서는 Credentials 항목을 true로 세팅하고 받는 쪽에서도 보내는 쪽은 출처를 정확히 입력한 후, Access-Control-Allow-Credentials 항목을 true로 맞춰줘야 더 안전한 공유가 가능합니다.
- Method와 Header에 Content-Type 등을 설정해줍니다.
- 이러한 GET, HEAD, POST 등의 요청을 simple request라고 하며
- PUT, DELETE, OPTIONS 등의 요청을 preflighted request이라고 하며, 다른 도메인의 리소스를 보내기 전 안전한지 확인하는 작업을 해줍니다. 허락이 되어야지 본격적인 요청을 보낼 수 있습니다. 서버의 데이터에 영향을 줄 수 있기 때문입니다.

[https://developer.mozilla.org/ko/docs/Web/HTTP/CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)