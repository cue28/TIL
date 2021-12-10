# defer, async 스크립트

스크립트 실행 시점을 조절할 수 있게 해주는 것이며,

- DOM을 따라 반드시 순서대로 실행되어야 한다면 `<script>`
- DOM이나 다른 스크립트에 의존성이 없고, 실행 순서가 중요하지 않은 경우라면 `<script async>`
- DOM이나 다른 스크립트에 의존성이 있고, 실행 순서가 중요한 경우라면 `<script defer>`

브라우저는 defer 속성이 있는 스크립트(이하 defer 스크립트 또는 지연 스크립트)를 '백그라운드’에서 다운로드 합니다. 따라서 지연 스크립트를 다운로드 하는 도중에도 HTML 파싱이 멈추지 않습니다. 그리고 defer 스크립트 실행은 페이지 구성이 끝날 때까지 지연 됩니다.

async 속성이 붙은 스크립트(이하 async 스크립트 또는 비동기 스크립트)는 페이지와 완전히 독립적으로 동작합니다. 페이지에 async 스크립트가 여러 개 있는 경우, 그 실행 순서가 제각각이 됩니다. 실행은 다운로드가 끝난 스크립트 순으로 진행

----

브라우저는 defer 속성이 있는 스크립트(이하 defer 스크립트 또는 지연 스크립트)를 '백그라운드’에서 다운로드 합니다. 따라서 지연 스크립트를 다운로드 하는 도중에도 HTML 파싱이 멈추지 않습니다. 그리고 defer 스크립트 실행은 페이지 구성이 끝날 때까지 지연 됩니다.

async 속성이 붙은 스크립트(이하 async 스크립트 또는 비동기 스크립트)는 페이지와 완전히 독립적으로 동작합니다. 페이지에 async 스크립트가 여러 개 있는 경우, 그 실행 순서가 제각각이 됩니다. 실행은 다운로드가 끝난 스크립트 순으로 진행합니다.

- [https://wormwlrm.github.io/2021/03/01/Async-Defer-Attributes-of-Script-Tag.html](https://wormwlrm.github.io/2021/03/01/Async-Defer-Attributes-of-Script-Tag.html)
- [https://kimlog.me/js/2019-10-05-script/](https://kimlog.me/js/2019-10-05-script/)