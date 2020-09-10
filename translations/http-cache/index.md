# HTTP Cache를 사용해서 불필요한 네트워크 요청을 방지하자

이 글 [https://web.dev/http-cache/](https://web.dev/http-cache/)을 번역했습니다.

리소스를 네트워크를 통해서 가져오는것은 느리고 비용이 큽니다:

- 큰 Response는 브라우저와 서버간 여러번의 왕복을 필요로 합니다.
- 주요 리소스들이 완전히 다운로드 되기 전에는 페이지가 로드 되지 않을 것입니다.
- 만약 사용자가 당신의 사이트를 제한된 요금제로 이용할 경우, 모든 불필요한 네트워크 요청은 그들의 돈을 낭비하는 것입니다.

어떻게 불필요한 네트워크 리쿼스트를 피할 수 있을까요? 브라우저의 HTTP Cache가 당신의 첫 방어선입니다!  
가장 강력하거나 유연한 방법이라고 할 수 없고, 당신은 캐시된 Response에 대해 제한적인 컨트롤 밖에 가지지 못하지만,Cache는 효과적입니다. 모든 브라우저가 캐시를 지원하고 있고, 캐시를 세팅하는데 큰 작업이 필요하지 않기 때문입니다.

이 가이드는 효과적인 HTTP Caching을 적용하기 위한 기본을 알려줄 것입니다.

## 브라우저 호환성

HTTP Cache라는 하나의 API는 존재하지 않습니다. 몇 웹 API들의 묶음을 일반적으로 Cache라고 부르는 것 뿐입니다.
이 API 들은 모든 브라우저에서 지원됩니다:

- [Cache-Control](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Cache-Control#Browser_compatibility)
- [ETag](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/ETag#Browser_compatibility)
- [Last-Modified](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Last-Modified#Browser_compatibility)

## HTTP 캐시는 어떻게 작동하나요

모든 HTTP 요청은 우선적으로 브라우저 캐시를 체크합니다. 해당 요청에 대해 캐시된 유효한 reponse가 있는지 확인하고 만약 있다면 Response를 캐시로부터 가져옵니다. 이것은 네트워크 왕복으로 생기는 네트워크 지연과 데이터 비용을 없애도록 해줍니다.

HTTP Cache의 행동은 Request 헤더와, Response 헤더에 의해 통제됩니다.  
이상적인 시나리오라면, 당신은 웹 어플리케이션의 코드와 (Request 헤더를 담당하는) 웹 서버의 코드 (Response 헤더를 담당하는) 양쪽에 대한 조정이 가능할 것입니다.

MDN의 [HTTP Caching](https://developer.mozilla.org/ko/docs/Web/HTTP/Caching)을 통해 더 깊이 있는 개념적인 설명을 읽어보세요.

## Request 헤더: 왠만하면 default를 따라라

당신의 웹 앱이 리퀘스트를 할때 중요한 헤더는 많이 있지만  
브라우저는 왠만하면 언제나 당신 대신에 해당 중요 헤더들을 리퀘스트에 적용해줄 것입니다.
데이터의 신선도를 체크하는 헤더들은 (EX: If-None-Match If-Modified-Since) 브라우저가 현재 캐시내에 있는 값들에 대한 정보를 바탕으로 적용여부가 결정됩니다.

이것은 좋은 소식입니다--당신이 `<img src="my-image.png">` 같은 태그를 사용하면 브라우저가 자동으로 캐싱처리를 해준다는 뜻이기 때문입니다.

## Response 헤더: 웹 서버를 설정하라

서버에서 캐싱관련해서 할수 있는 가장 중요한 셋업은 Response 헤더이다. 이 헤더들은 모두 효과적인 캐싱에 중요한 역활을 한다:

- Cache-Control. 서버는 Cache-Control 지시어(directive)를 통해 브라우저와 다른 중간 cache들이 어떻게, 얼마나 오래 캐싱을 할지 정할 수 있다.
- ETag. 브라우저가 만료된 캐시 Response를 확인한다면, 작은 토큰을 (보통 파일 컨텐트의 hash를 사용한다) 서버에 보내 파일이 변했는지 확인한다. 만약 서버가 같은 토큰을 돌려준다면, 그 파일은 바뀌지 않았기 때문에 다시 다운로드 할 필요가 없다.
- Last-Modified. 이 헤더는 Etag와 비슷한 목적으로 사용되지만, 수정 시간을 기반으로 해당 리소스가 바뀌었는지 체크한다. 이것은 Etag의 컨텐트 기반 체크방식과 대비된다.

어떤 웹 서버들은 default로 캐싱관련 해더들을 적용하는 반면, 어떤 웹 서버들은 전혀 적용하지 않기도 한다. 헤더를 설정하는 방법은 웹 서버마다 다 다르기 때문에 해당 웹 서버의 문서를 참고 하는게 가장 정확하고 좋을거다.

당신의 시간을 아껴드리기 위해, 여기 유명한 웹 서버들을 설정하는 방법을 알려주는 링크를 남긴다.

- Express
- Apache
- nginx
- Firebase Hosting
- Netlify

Cache-Control Response 헤더를 적용하지 않는 것은 HTTP Caching을 비활성화 하지 않는다!  
브라우저는 특정 컨텐트에 어떤 캐싱 행동이 적합할지를 추정하고 알아서 적용시킨다.
아마도 당신은 자동으로 설정해주는 것보다 고도화된 컨트롤을 바랄 것이다, 그러므로 시간을 투자해 당신의 Response 헤더를 설정하는것을 권장한다.
