[참고 링크] https://developer.chrome.com/docs/devtools/tips?hl=ko
[CWV] https://web.dev/articles/vitals?hl=ko
# Tips 1 : Record and analyze a performance trace
## Setting
크롬 성능 측정 시 시크릿 모드 실행
Performance > Environment serrings > Network 속도 'Fast 4G'로 변경

<br/>

## Web Vitals
: 웹 성능 지표

* FCP, First Contentful Paint
: 첫 번째 콘텐츠가 표시되는 시간

* TTI, Time To Interactive
: 사용자 인터렉션이 가능할때까지 걸리는 시간

* SI, Speed Index
: 페이지가 표시되는 속도

* TBT, Total Blocking Time
: 첫 번째 콘텐츠가 표시되고 사용자가 인터렉션이 가능해지는 시간동안 메인 스레드를 블로킹하는 작업 시간

* LCP, Largest Contentful Paint
: 가장 마지막으로 콘텐츠가 표시되는 시간(최대 콘텐츠 렌더링 시간)

* CLS, Comulative Layout Shift
: 누적 레이아웃 이동(시각적 안정성 지표)

<br/>

## CWV, Core Web Vitals
* LCP, Largest Contentful Paint
: 최대 콘텐츠 렌더링 시간
* INP, Interaction to Next Paint
: 다음 페인트에 대한 상호작용
* CLS, Cumulative Layout Shift
: 누적 레이아웃 변경

<img src="https://web.dev/static/articles/vitals/image/largest-contentful-paint-ea2e6ec5569b6.svg?hl=ko" width="300"/>
<img src="https://web.dev/static/articles/vitals/image/inp-thresholds.svg?hl=ko" width="300"/>
<img src="https://web.dev/static/articles/vitals/image/cumulative-layout-shift-t-5d49b9b883de4.svg?hl=ko" width="300"/>

<span style="color:darkgray">[이미지 출처] https://web.dev/articles/vitals?hl=ko</span>

## HTML 속도 향상을 위한 방법
* 리디렉션 최소화
: 리디렉션은 페이지 로딩 속도를 저하시킬 수 있다.
특히 동일한 도메인 내에서 발생하는 리디렉션은 서버 설정을 통해 제어할 수 있으므로, 이러한 리디렉션을 줄이는 것이 좋습니다.

* HTML 응답 캐싱
: HTML 파일을 캐시에 저장하면, 서버 부하를 줄이고 페이지 로딩 시간을 단축할 수 있습니다.   다만, 사용자별로 개인화된 콘텐츠를 제공하는 경우에는 캐싱 설정에 주의해야 합니다.

* 서버 응답 시간 측정하기
: 서버의 응답 시간은 페이지 로딩 속도에 직접적인 영향을 미칩니다.  
서버 타이밍 헤더를 활용하여 인증, 데이터베이스 접근 등 각 단계별 소요 시간을 측정하고, 이를 기반으로 최적화를 진행할 수 있습니다.

* HTML 파일 압축
: HTML, CSS, JavaScript와 같은 텍스트 기반 리소스는 압축을 통해 전송 크기를 줄일 수 있습니다.  
Brotli와 gzip과 같은 압축 알고리즘을 사용하면 네트워크 대역폭을 절약하고 로딩 시간을 단축할 수 있습니다.

* CDN 활용
: CDN은 전 세계에 분산된 서버를 통해 사용자와 가까운 위치에서 콘텐츠를 제공하여 로딩 시간을 단축시킵니다.

>> [학습중인 부분] https://web.dev/learn/performance/general-html-performance

<!-- 
# HTML 헤더
* ETag(Entity Tag)
서버 응답의 최신성 확인
웹페이지 최초 진입 : ETag + 전체 응답

*  -->