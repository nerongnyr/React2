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

### 241113

7.1 UI라이브러리

- UI 라이브러리, 프레임워크, 유틸리티 기능이 필수는 안닙니다
- 다만 생산성 향상 및 UI의 일관성을 유지하는데 많은 도움을 받을 수 있습니다
- 이번 장에서는 다음 3가지의 프레임워크에

7.2 Chakra UI

- 오픈소스 컴포넌트 라이브러리로, 모듈화되어있고 접근성이 뛰어나며 보기 좋은 UI를 만들 수 있습니다
- 버튼, 모달, 입력 등 다양한 내장 컴포넌트를 제공합니다
- dark mode, light mode 모두 지원
- Chakra UI의 useColorMode 훅을 사용해서 현재 사용하는 컬러 모드를 확인할 수 있습니다
- 기본 컴포넌트를 조합해서 새로운 컴포넌트를 쉽게 만들 수 읶습니다

7.3 Taiwind CSS

- 다른 프레임워크와는 다르게 css 규칙만을 제공합니다
- 자바스크립트 모듈이나 리액트 컴포넌트를 제공하지 않기 때문에 필요한 경우 직접 만들어서 사용해야 합니다
- 변수값을 조정하여 개성있는 디자인을 만들 수 있습니다/ 디자인의 자유도가 높숩니다
- dark mode, light mode 모두 지원
- 빌드 시점에 사용하지 않는 클래스는 제거되기 떄문에 높은 수준의 최적화를 지원합니다
- CSS 클래스의 접두사를 활용해서 모바일, 데스크톱, 테블릿 화면에서 원하는 규칙을 지정할 수 있습니다. sm(649px), md(768px), lg(1024px), xl(1280px), 1xl(1536px)

7.4 Headless UI

- TailwindCSS를 만든 Tailwind Labs 팀의 무료 오픈소스 프로젝트
- TailwindCSS는 웹 컴포넌트 안에서 사용할 수 있는 CSS클래스만 제공
- 따라서 모달이나 버튼 등 동적인 컴포넌트를 만들려면 직접 자바스크립트 코드를 작성해야 함
- 이런 단점을 보완하기 위해 Headless UI 를 만듦

1. Project 생성

- Tailwind 사용을 위해 프로젝트를 다시 생성합니다
- 프로젝트를 다시 생성하지 않고 설정할 수도 있지만 과정이 다소 복잡합니다
- 프로젝트를 Next.js 14로 합니다
- 15.0.2 버전이 릴리즈 되어있으나 아직 Tailwind와의 호환성이 안정적이지 않습니다
- $ npx create-next-app@14
- 프로젝트 이름은 자유로 하고, 나머지는 모두 yes로 합니다

2. Tailwind CSS

- React 기준으로 하고 있어서 바로 코드를 사용하면 오류가 발생할 수 있ㅇ,ㅁ
- Test코드는 tailwindcss.com에 나와있는 것잉 오류가 적다
- class 도 className으로 수정

3.Headless UI

4. Chakra UI

### 241120

Props 흐름의 이해

- Next.js의 데이터 흐름은 단방향으로 이루어집니다
- 즉, parents에서 child component의 방향으로 props의 흐름이 이루어 집니다
- 따라서 계층 구조가 복잡해지면 Props Drilling은 문제가 발생합니다
- Props Drilling은 여러 개의 component를 지나 props가 전달되면서 발생하는 문제입니다

- Props Drilling은 다음과 같은 문제를 발생시킬 수 있습니다
  1. 중간에 위치한 component에 불필요한 props를 전달해야하는 문제
  2. 타겟 component까지 props가 전달되지 않을 경우 원인 규명의 어려움
  3. 필요 이상으로 코드가 복잡해지는 문제
- 이런 문제를 해결하려면 props를 전역으로 사용하면 됩니다

Props 흐름의 이해

- Component A,B,c, props-flow 페이지 상호간에는 계층구조를 가지고 있지 않습니다
- 아직 어느 쪽에서도 component 호출하지 않았기 떄문입니다
- 그러나 어느 쪽이는 component를 호출하는순간, 호출한 쪽은 parent가 되고, 호출받은 쪽은 child가 됩니다
- 이것은 component간, comonent와 page간 모두에 적용됩니다
- 관계가 한번 성립되면 child가 parent를 호출할 순는 없습니다
- 예를 들어 A가 B를 호출한 경우, A는 parent, B는 child가 됩니다
- 이 관계는 아직 아무도 호출하지 않거나, 호출받지 않은 C에게는 적용되지 않습니다

2. Context API 개요

- Context는 UI구축에 많이 사용되는 React의 기능입니다
- React는 16.3버전부터 정식적으로 context api 를 지원하고 있습니다
- 일반적으로 props는 부모에서 자식으로 전달되는 단방향 통신을 합니다
- Context API는 특정 component가 props를 사용하지 않고, 하위 component를 포함한 모든 component에 데이터를 공유할 수 있는 기능을 제공합니다
- 간혹 Cunsumer를 useContext대신 사용하는 경우가 잇지만, function형 component에서는 많이 사용하지 않습니다
- 두가지의 차이는 다음과 같습니다

- Consumer    -useContext
  1. 사용: 클래스형, 함수형 모두 사용 가능 /  함수형 컴포넌트에서 주로 사용
  2. 문법: JSX 내에서 명시적으로 작성  /  Hook으로 간결하게 사용
  4. 장점: 클래스형 컴포넌트의 호환성 ?
  5. 단점
 
2. Context API - use client

- Next.js에서 'use client'를 사용하는 이유는 서버 컴포넌트와 클라이언트 컴포넌트를 구분하기 위해서입니다

3. 주요 Directory & File

3.1 Directory 구조

[ Directory ]

- app : Routing page 관리
- components : 재사용 가능한 공통 컴포넌트 관리,
  애플리케이션 전반에서 재사용될 수 있는 공통 컴포넌트를 보관합니다,
  특정 기능에 종속되지 않으며, 다양한 페이지나 기능에서 재사용할 수 있는 component를 모아둡니다
- context : context 컴포넌트 관리
- features : 기능별 컴포넌트 관리,
  특정 기능이나 도메인 별로 코드를 구성하는 데 사용합니다,
  사용자 인증 기능. 프로필 관리 기능 등 각 기능관 관련된 상태 관리, API 요청, 슬라이스, 컴포넌트 등을 보관합니다,
  재사용이 불가능하거나 가능하더라도 많은 수정을 해야 하는 컴포넌트를 관리합니다.
- store : Redux store 설정 파일 관리
- styles : CSS, Sass 등 스타일 파일 관리

3.2 Redux 주요 File의 역할

[ Redux Slice ]

- Slice는 Redux Toolkit에서 사용되는 용어로, 특정 기능과 관련된 상태와 reducer함수의 모음을 나타냅니다
- Slice라는 이름은 애플리케이션 상태의 한 부분을 의미합니다
- Redux Toolkit의 createSlice함수를 사용하면 특정 기능과 관련된 상태, 액션, reducer를 한 곳에서 정의할 수 있어 관리하기가 용이합니다

[ Redux Provider ]

- Redux Provider 는 Redux의 상태 등을 공급하기 위한 파일입니다
- Provider는 사용하고자 하는 Page에서 사용하면 됩니다
- 다만 전역적으로 사용할 때 layout파일에 정의하면 'use client'를 사용해야하기 때문에 별도의 component로 만들어서 사용하는 것이 좋습니다

4. Context API vs. Redux

[ Context API ]

- React에서 기본으로 제공하는 상태 고나리 도구로, 외부 라이브러리 성치 없이 사용 가능합니다
- Context API 는  주로 전역 상태를 관리하는 데 사용됩니다
- React.createContext()로 생성한 Context 객체와 Provider 컴포넌트를 사용해 상태를 하위 컴포넌트에 전달합니다

( 장점 )

- 간단하고 가볍다: 외부 라이브러리 설치 없이 기본 React 기능만으로 전역 상태 관리를 할 수 있습니다
- 적은 설정 필요: 간단한 구조를 가지고 있어 설정과 사용이 간편합니다
- 컴포넌트 트리의 깊이 제한 없음: 여러 단계에 걸처 상태를 전파할 수 있어 prop drilling 문제를 해결합니다

( 단점 )

- 복잡한 상태 관리에 한계: 상태가 복잡하거나 다양한 액션을 통해 변경이 이루어져야하는 경우, 관리가 어려워질 수 있습니다
- 성능 문제: 상태가 업데이트되면 해당 상태를 사용하는 모든 하위 컴포넌트가 다시 렌더링되므로, 상태 범위가 넓을 경우 성능에 영향을 미칠 수 있습니다
- 디버깅 도구 부족: 상태 변경 과정을 추적하고 관리하는 Redux DevTools와 같은 도구가 기본적으로 제공되지 않습니다

[ Redux ]

- Redux는 전역 상태를 관리하기 위한 독립적인 state 관리 라이브러리입니다
- 상태의 변경을 예측 가능하게 하고, 전역 state 관리를 더 구조적으로 지원합니다
- store, reducer, action 등의 개념을 사용해 state와 state dispatch를 관리합니다

( 장점 )

- 명확한 상태 관리 구조: 액션과 reducer를 통해 state dispatch 과정을 예측 가능하게 만들고, 코드의 가독성을 높입니다
- 미들웨어 지원: redux-thunk, redux-saga와 같은 미들웨어를 사용해 비동기 로직을 쉽게 처리할 수 잇습니다
- 디버깅 도구: Redux DevTools를 통해 상태 변화 및 디버깅이 용이합니다
- 모든 프레임워크와 호환: React 뿐만 아니라 다른 JavaScript 프레임워크와도 함께 사용할 수 있습니다

( 단점 )

- 설정과 코드 복잡도: Context API 에 비해 설정이 복잡하며, boilerplate 코드가 많이 필요합니다
- 추가 라이브러리 필요: Redux 자체가 외부 라이브러리이므로 설치 및 유지 관리가 필요합니다
- 작은 애플리케이션에는 과한 설정: 단순한 상태 관리가 필요한 작은 애플리케이션에서는 과도한 설정일 수 있음

항목 | Context API | Redux
규모 작은규모 대규모
복잡성 간단한 상태 복잡한 상태
학습 난이도 낮음 높음
성능 상황에 따라 다름 비교적 안정적
유연성 낮음 높음
디버깅 도구 기본적으로 없음 Redux

1.1 GitHub Pages 기본 저장소 생ㅅ어

- 내용 없어도 됨
- 외부에서 <MyID>.github.io
