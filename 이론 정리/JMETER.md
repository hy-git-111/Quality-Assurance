# JMeter
* 지원 프로토콜
    * Web  : HTTP, HTTPS (Java, NodeJS, PHP, ASP.NET, …)
    * WebServices  : SOAP / REST
    * Database via JDBC
    * FTP, LDAP, JMS, Mail (SMTP, POP3, IMAP), TCP, OS Native processes 등

* GUI모드의 경우 메모리, CPU 사용량이 많아 대규모 실행 시 CLI 모드 사용 권장
* API 부하테스트 전용 툴, SPA 테스트는 어려움

## CLI 모드
* 실행 명령어
    ```
    터미널에서 실행
    jmeter -n -t <testplan.jmx> -l <results.jtl> -e -o <report_output_dir> 
    ```

* 명령어 옵션
    * -n  : Non-GUI 모드
    * -t  : Test Plan(.jmx) 지정
    * -l  : 결과 파일(.jtl) 저장 경로 지정
    * -e  : 테스트 종료 후 HTML 리포트 생성
    * -o  : HTML 리포트를 저장할 빈 디렉터리 지정

## GUI 모드
* 실행 방법
    * Windows  : jmeter.bat 실행(apache-jmeter-5.6.3\bin\jmeter.bat)
    * Linux/macOS  : 터미널에서 명령어로 실행(apache-jmeter-5.6.3\bin\jmeter.sh)
        ```
        cd apache-jmeter-5.6.3\bin
        jmeter.sh
        ```
### 구성 요소
* Test Plan
: 테스트 요소(Element)들을 논리적으로 그룹화

* Thread Group
: 가상 사용자 그룹 정의, JMeter 실행 시 Thread Group 단위로 실행됨

    ![alt text](img\image-17.png)

* Sampler
: 실제 요청을 생성하여 서버로 전송

    * HTTP Request  : HTTP 요청 전송
    * FTP Request : FTP 서버 파일 업로드/다운로드
    * JDBC Request : 데이터베이스 쿼리 실행
    * TCP Sampler : TCP 소켓 통신 테스트
    * SMTP Sampler : 이메일 발송 테스트

* Config Element
: 요청에 필요한 기본값 설정
    * HTTP Header Manager : HTTP 요청 헤더 설정
        ```
        e.g.
        Content-Type: application/json
        Authorization: Bearer ${token}
        ```
    * HTTP Request Defaults : HTTP 요청의 기본값 설정    
    * HTTP Cookie Manager : 서버로부터 받은 Set-Cookie 헤더를 저장하여 이후 자동 전송
    * CSV Data Set Config : 외부 CSV 파일에서 데이터를 읽어와 동적 파라미터로 사용
    * User Defined Variables : 테스트 계획 내에서 사용할 변수 정의
    ```
    e.g.
    Name: targetHost, Value: www.google.com
    > 이후 ${targetHost} 형식으로 변수 사용 가능
    ```

* Listener
: 요청 결과를 수집, 분석 및 시각화
    * View Results Tree : 각 요청/응답 상세 정보 확인, 디버깅용
    * Summary Report : 전체 통계 요약 (Avg, Min, Max, Error%, Throughput 등)
    * Aggregate Report : Summary Report와 유사 + Percentile 정보
    * Backend Listener : 결과를 외부 시스템(InfluxDB 등)으로 전송 (실시간 모니터링)

* Assertions
: Sampler의 응답 검증  
    > <span style="color:darkgray">**일반적인 부하테스트는 리턴값을 검증하지 않는다.  
    API 성능 테스트의 경우 응답값을 확인한다.**</span>

    * Response Assertion : 응답 코드, 텍스트 내용, 헤더 등을 검증
    ![alt text](img\image-18.png)

    * Duration Assertion : 요청의 최대 허용 응답 시간 검증
    * Size Assertion : 응답 크기를 검증

* Timer
: Think Time 입력, Timer는 모든 Sampler 실행 전에 적용됨
    * API 순차 실행 확인 가능
    * API 개폐 시점으로 인한 오버플로우 확인 가능

## 주요 지표와 권장값

|지표|설명|기준값(권장)|참고
|:---|:---|:---|:---|
|Average Response Time|평균 응답 시간|≤ 1초 (1000ms)|사용자 경험 향상
|Median (50th Percentile)|중앙값 응답 시간|평균과 유사해야 함|응답 시간의 일관성 확인
|90th Percentile|상위 90% 응답 시간|평균의 1.5배 이내|응답 시간의 일관성 확인
|Standard Deviation|응답 시간의 표준 편차|평균의 50% 이하|응답 시간의 안정성 평가
|Error %|실패한 요청의 비율|0%|안정성 확보
|Throughput|초당 처리 요청 수 (TPS)|높을수록 좋음|시스템 처리 능력 평가
|Latency|요청 후 첫 응답까지의 시간|낮을수록 좋음|네트워크 지연 확인
|Connect Time|연결 수립 시간|낮을수록 좋음|서버 연결 속도 평가
