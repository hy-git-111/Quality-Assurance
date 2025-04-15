# 필수 설치 명령어
npm install -g newman
npm install --reporter-html-export

# 실행 명령어
newman run .\Runner_test.postman_collection.json -e '.\New Environment.postman_environment.json' -n 3 -d .\Runner_test.postman_collection.json -r html --reporter-html-export report.html

## 실행 명령어 뜻
newman run 컬렉션.json 
-e 환경변수.json 
-n 반복횟수 
-d 데이터파일.json 
-r 리포트 형식 --reporter-html-export 리포트파일명.html