# React2

## 202230109 나예린

### 240904

1. Next.js

### 240911

2. 렌더링 전략

* 렌더링 전략이란 웹 페이지 또는 웹 애플리케이션을 웹 브라우저에 제공하는 방법을 의미합니다
* 정적인 페이지 제작에는 Gatsby를 추천합니다.
* 서버 사이드 렌더링 전략을 원한다면 다른 프레임워크를 검토

2.1. 서버 사이드 렌더링(SSR)

* 생소할 수 있지만 웹 페이지를 제공하는 가장 흔한 방법입니다
* APM을 이용하는 일반적인 웹 페이지 생성이라고 보면 됩니다.
* 여기에 자바스크립트 코드가 적재되면 동적으로 페이지 내용을 렌더링합니다

* Next.js도 이와 같이 동적으로 페이지를 렌더링할 수 있습니다.
* 그리고 여기에 스크립트 코드를 집어 넣어서 나중에 웹 페이지를 동적으로 처리할 수도 있는데 이를 하이드레이션이라고 합니다.

* 예를 들면 어떤 사람이 작성한 블로그 글을 한 페이지에 모아서 작성해야 한다면 SSR을 이용하는 것이 적당합니다.
* 서버 사이드 렌더링 -> 자바스크립트가 하이드레이션된 페이지를 전송-> 클라이언트에서 DOM 위에 각 스크립트 코드를 하이드레이션: 페이지 새로 고침 없이 사용자와 웹 페이지간 상호작용을 가능하게 합니다

[ SSR의 장점 ]

* 더 안전한 웹 애플리케이션: 쿠키 관리, 주요 API, 데이터 검증 등과 같은 작업을 서버에서 처리하기 떄문에 중요한 데이터를 클라이언트에 노출할 필요가 없기 떄문입니다
* 더 뛰어난 웹 사이트 호환성: 클라이언트 환경이 자바스크립트를 사용하지 못하거나 오래된 브라우저를 사용하더라도 서비스를 제공할 수 있습니다.

SSR이 최적의 렌더링 전략이 아닌 경우

* 클라이언트가 페이지를 요철할 때마다 페이지를 다시 렌더링할 수 있는 서버가 필요합니다.
* 다를 방식에 비해 SSR이 더 많은 자원을 소모하고, 더 많은 부하를 보이며 유지 보수 비용도 증가합니다.
* 페이지에 대한 요청을 처리하는 시간이 길어집니다.
* 페이지가 외부 API 또는 데이터 소스에 접근해야 한다면, 해당 페이지를 렌더링할 때마다 이를 다시 요청해야 합니다.
* 페이지 간의 이동은 CSR에 비해 느립니다

* 중요한 것은 Next.js가 기본적으로 빌드 시점에 정적으로 페이지를 만든다는 것입니다.
* 페이지에서 외부 API를 호출하거나 데이터베이스에 접근하는 등 동적 작업을 해야 한다면 해당하는 함수를 페이지에 export 해야 합니다.

2.2 클라이언트 사이드 렌더링(CSR)

* React앱을 실행하면 렌더링 시작 전에 빈 화면이 한동안 유지되는 것이 보입니다.
* 이는 서버에서 스크립트와 스타일만 포함된HTML을 전송하기 떄문입니다.
* 실제 렌더링은 클라이언트에서 이루어집니다
* CSR로 생성한 앱의 HTML을 보면 div태그 하나밖에 없습니다. 그래서 빈 화면만 보였던 것입니다
* 빌드 과정에서 js와 css파일을 HTML페이지에 불러오도록 만들고 root div에 렌더링합니다

2.3 정적 사이트 생성(SSG:Static Site Generation)

* SSG는 일부 또는 전체 페이지를 빌드 시점에 미리 렌더링합니다
* SSG는 SSR 및 CSR과 비교했을 때 다음과 같은 장점이 있습니다.

    1. 쉬운 확장
    정적 페이지는 단순 HTML 파일이므로 CDN을 통해 파일을 제공하거나, 캐시에 저장하기 쉽습니다.
    2. 뛰어난 성능
    빌드 시점에 HTML 페이지를 미리 렌더링하기 떄문에 페이지를 요청해도 클라이언트나 서버가 무언가를 처리할 필요가 없습니다.
    3. 더 안전한 API 요청
    외부 API를 호출하거나, 데이터베이스에 접근하거나, 보호해야 할 데이터에 접근할 일이 없습니다.
    필요한 모든 정보기 빌드 시점에 미리 페이지로 렌더링 되어있기 때문입니다.


* SSG는 높은 확장성과 뛰어난 성능을 보이는 프런트엔드 애플리케이션을 만들고싶을 대 가장 좋은 방법입니
* 한 가지 문제점은 일단 웹 페이지를 만들고 나면 다음 배포 전까지 내용이 변하지 않는다는 것입니다
* 조금이라도 수정하려면 필요한 데이터를 가져와서 수정하고 다시 생성하는 과정을 반복해야 합니다.
* 이런 문제 떄문에 나온 방법이 바로 "증분 정적 재생성(ISR)"입니다
* 예를 들어 동적 콘텐츠를 제공하지만 해당 콘텐츠 데이터를 로딩하는데 시간이 오래 걸린다면, SSG와 ISR을 함께 사용하여 문제를 해결할 수 있습니다.
* 많은 양의 데이터를 필요로 하는 복잡한 대시보드를 만든다면, 데이터를 불러오기 위한 REST API 호출에 수 초가 소요됩니다
* 만일 데이터가 자주 변하지 않는다면 10분

### 241011

1. Page Project Layout -_app

- _app.jsx는 서버에 요청할 떄 가장 먼저 실행되는 컴포넌트입니다
- 페이지에 적용할 공통 레이아웃을 선언하는 곳입니다

Page Project Layout -_document

2. App Project Layout - layout.jsx

App Project Layout - meta data

- metadata에서 모든 페이지에 적용할 meta data를 선언할 수 있습니다
- title의 경우에는 각 페이지에 맞게 작성하는 것이 SEO 에 좋습니다

App Project Layout - LootLayout

App Project Layout - Link component

3. Link vs. a vs. router.push

- Link component를 이용해서 Navibar component를 만들어봅니다.
- <a> tag는 html 동기식으로 전체기 reload 되기 때문에, 외부 링크를 할 떄 사용합니다
- 일반적으로 내부 링크 이동시에는 사용하지 않는 것이 좋습니다

- router.push 는 빌드 후, 이동할 주소가 html 상에 노출되지 않기 때문에 SEO 에 취약합니다

- Link 컴포넌트는 빌드 후, a tag로 자동 변환됩니다
- a tag의 장점인 SEO 최적화, prefetch 가능, 우 클릭 기능 등을 갖습니다.
- 내부 페이지로의 이동할 때 이 방식을 사용해야 SPA 방식으로 전체 html 중 필요한 부분만 비동기식으로 리렌더링 된다



1. Image component -local

- 정적 자원 중 이미지 파일은 SEO에 많은 영향을 미핍니다.
- 다운로드시간이 많이 걸리고, 렌더링 후에 레이아웃이 변경되는 등 UX에 영향을 미칩니다
- 이것을 누적 레이아웃 이동(CLS: Cumulative Layout Shift)라고 합니다
- Image컴포넌트를 사용하면 CLS문제를 해결합니다
- lazy loading: 이미지 로드 시점을 필요할 떄까지 지연시키는 기술입니다
- 이미지 사이즈 최적화로 사이즈를 1/10 이하로 줄여줍니다
- Placeholder를 제공합니다
- WebP와 같은 최신 이밎 포맷 및 최신 포맷을 지원하지 않는 브라우저를 위해 png나 jpge 와같은 예전 이미지 포맷도 제공합니다
- Pixabay나 Unplash와 같은 외부 이미지 서비스로 이미지를 제공할 수 있습니다
- Image 컴포넌트를 사용하면 다양한 props를 전달할 수 있습니다
    ** 주요 props **
    - src = " "
    - width = {500}
    - height = [500}
    - alt = ""
    - Placeholder = "blue"
      // 외부 이미지는 blurDataURL=''로 처리
    - loading = "lazy"
- 정적 자원은 기본적으로 public 디렉토리에 저장합니다
 
### 241023
 
1. Static Resource

- 정적 자원 중 이미지 파일은 SEO 에 많은 영향을 미칩니다
- 다운로드 시간이 많이 걸리고, 렌더링 후에 레이아웃이 변경되는 등 UX에 영향을 미칩니다
- 이것을 누적 레이아웃 이동(CLS:Cumulative Layout Shift)이라고 합니다
- Image 컴포넌트를 사용하면 CLS문제를 해결합니다
- lazy loading: 이미지 로드 시점을 필요할 때까지 지연시키는 기술입니다
- 이미지 사이즈 최적화로 사이즈를 1/10이하로 줄여줍니다
- Placeholder를 제공합니다

04. 코드 구성과 데이터 불러오기
- 애플리케이션의 디렉터리 구조를 어떻게 구성하는지 알아봅니다
- 클라이언트와 서버에서 외부 REST 및 GraphQL API를 사용하는 방법도 알아봅니다

컴포넌트 구성

- 컴포넌트는 세 가지로 분류하고 각 컴포넌트와 관련된 스타일 및 테이스 파일을 같은 곳에 두어야 함
- 코드를 더 효율적으로 구성하기 위해 아토믹 디자인 원칙에 따라 디렉토리를 구성
- atoms: 가장 기본적인 컴포넌트 관리. 예) button,input,p와 같은 표준 HTML요소를 감싸는 용도로 사용되는 컴포넌트
- molecules: atom에 속한 컴포넌트 여러 개를 조합하여 복잡한 구조로 만든 컴포넌트 관리. 예) input 과 label을 합쳐서 만든 새로운 컴포넌트
- organisms: molecules와 atomes를 섞어서 더 복잡하게 만든 컴포넌트 관리. 예)footer나 carousel 컴포넌트
- templates: 위의 모든 컴포넌트를 어떻게 배치할지 결정하여 사용자가 접근할 수 있는 페이지

유틸리티 구성

- 컴포넌트를 만들지 않는 코드 파일
- 렌더링에 필요한 컴포넌트가 아닌 기타 필요한 스크립트가 있다면, utilities/디렉토리에 별도로 보관
- 예) 애플리케이션의 log파일을 저장하는 코드
- 각 유틸리티에 맞는 테스트 파일도 만듦

정적 자원의 구성

- public/ 디렉토리에서 관리
- 일반적인 웹 애플리케이션에서는 다음과 같은 정적 자원 사용

스타일 파일 구성

- 스타일 파일은 앱에서 어떤 스타일 관력 기술을 사용하는가에 따라 구성 달라짐
- Emotion, styled-components,JSS와 같은 CSS-in-JS 프레임워크의 경우 컴포넌트별로 스타일 파일을 만듦. 이렇게 하면 스타일 변경 쉽다
- 만일 컬러 팔레트, 테마, 미디어 쿼리와 같은 공통 스타일의 경우는 styles/ 디렉토리를 사용함

lib 파일 구성

- lib 파일은 서드파티 라이브러리를 감싸는 스크립트를 말한다

4.2 데이터 불러오기

- Next는 클라이언트와 서버 모두에서 데이터를 불러올 수 있다
- 서버는 다음 두 가지 상황에서 데이터를 불러올 수 있음
  1) 정적 페이지를 만들 때 getStaticProps 함수를 사용해서, 빌드 시점에 데이터를 불러올 수 있음
  2) 서버가 페이지를 렌더링할 떄 getServerSideProps를 통해, 실행 도중 데이터를 불러올 수도 있음
- 데이터 베이스에서 데이터를 가져올 수도 있지만 안전하지 않기 때문에 권장하지 않음. 데이터베이스 접근은 백엔드에서 처리하는 것이 좋음

### 241030

서버에서 REST API 사용하기

1. REST API

- REST(Representational State Transfer) 란 자원을 이름으로 구분하여 그 자원의 상태를 통신을 통해 주고 받는 것을 의미합니다

2. Json Server

- Backend가 개발되기 전이나, 아직 외부 API 가 결정되지 않았다면 local 에 Json server를 구축하고 Frontend 개발을 하기에 적합한 node 패키지입니다.

3. Axios


