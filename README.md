# 마약범죄 판례 조회 서비스

## 개요
마약이 우리 사회 전체로 급속히 확산하고 있는 양상이다.
최근 정부에서는 '마약과의 전쟁'을 선포할만큼 이 문제를 심각히 여기고 있다.
경찰청에 따르면 2018년 12,613명이었던 마약사범은 2021년에는 16,153명으로 크게 증가한 것으로 나타났다.
하지만 이렇게 급증하는 마약범죄에도 불구하고, 사람들은 유명인 또는 재벌 '마약 스캔들'에만 주목할 뿐 그 이상 관심을 두지 않는듯 하다.
또한, 마약범죄와 관련한 구체적인 정보를 제공하는 기관은 현재 몇개의 판례 검색 사이트를 제외하면 국내에서 찾아보기 드물다.
따라서, 마약범죄 판례 조회 서비스는 이와 같은 사회적 분위기 속에서 출발했다.
본 서비스의 목적은 먀약범죄에 관한 다양한 정보 제공에 있다.
마약범죄 판례 조회 서비스는 과거 마약에 관한 판례 데이터를 수집하고, 수집한 데이터를 바탕으로 마약의 종류별 형량 분포와 판례를 제공한다.
본 서비스는 형량의 분포에 따라 판례를 제공하고 있기 때문에, 기존의 다른 판례 검색 서비스보다 구체화된 결과를 제공한다.
 
## 개발 환경
 * Python 3.8.15
 *  Selenium 3.141.0
 * Django 4.0.3
 
 ## 주요 내용
 ### 1. 데이터 수집
 * 데이터는 국내 최다 판례 조회 사이트인 빅케이스(<https://bigcase.ai>)에서 수집을 진행하였다.
 * Selenium 패키지를 사용해 동적 웹크롤링 방식으로 데이터 수집을 진행하였다.
 * 사이트로부터 7,259개의 판례 원문 데이터를 수집하였다.
 * 총 10가지의 마약과 관련된 판례 원문 데이터를 수집하였다.
 
 ### 2. 데이터 전처리
 * 서비스를 구현을 위해 판례 원문으로부터 다음 5가지 특징을 추출하였다.
 1) 사건번호: 판례 고유 번호
 2) 취급마약: 판례가 어떤 마약에 관한 판례인지를 나타냄. 
 3) 형종: 형량의 종류
 4) 형량범위: 형량의 범위
 5) 범죄사실: 선고에 적용된 범죄사실을 나타냄.
 * 전처리를 완료한 데이터 테이블의 모습은 다음과 같다.
 <img width="1280" alt="데이터 테이블" src="https://user-images.githubusercontent.com/121072239/212743274-4c37842c-075f-47cd-ac03-1db76795afc0.png">


 ### 3. 서비스 구현
 * 서비스는 웹사이트 형태로 구현하였으며, Django 프레임워크를 사용해 구현하였다.
 * 본 서비스는 정식으로 배포되지 않았기 때문에, 로컬 서버에서만 구동이 가능하다.
 * 구동 방법은 다음과 같다.
 1) 개발환경에 맞는 가상환경을 실행한다.
 2) 터미널 경로를 첨부한 myweb 폴더로 변경한다.
 3) python manage.py runserver 명령을 실행한다.
 4) 출력된 로컬 서버로 웹사이트를 통해 접속한다.

 ### 4. 서비스 주요 기능
 * 사용자가 입력한 마약에 따라 형종별, 형량별 판례 데이터 분포와 분포에 해당하는 판례 원문을 조회할 수 있다.
 * 사이트 내 존재하는 판례 데이터의 마약별 분포를 조회할 수 있다.

## 결과
* 구현한 서비스의 모습은 다음과 같다.
<img width="1280" alt="홈페이지" src="https://user-images.githubusercontent.com/121072239/211204990-3de72f94-d781-408a-bfeb-4148b8bcc904.png">
<img width="1280" alt="마약별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/211205400-2a02f31b-d3c2-4d2f-ab57-a743ae653314.png">
<img width="1280" alt="검색 페이지" src="https://user-images.githubusercontent.com/121072239/211205594-0e37f3d2-0919-4bf4-9550-cc3d91abd771.png">
<img width="1280" alt="형종별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/211205427-f9a74b34-ef44-4fab-a583-e3babc66416b.png">
<img width="1280" alt="형량별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/211205602-b664ad16-ae7d-4b92-ab30-0db92a1c8bb0.png">
<img width="1280" alt="판례 원문 페이지" src="https://user-images.githubusercontent.com/121072239/211205445-7e1322dd-1d48-40dc-915e-63140414e482.png">
