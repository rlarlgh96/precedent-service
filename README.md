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
 * Selenium 3.141.0
 * Django 4.0.3
 
## 주요 내용
 ### 1. 데이터 수집
 * 데이터는 국내 최다 판례 조회 사이트인 빅케이스(<https://bigcase.ai>)에서 수집을 진행하였다.
 * Selenium 패키지를 사용해 판례 원문을 크롤링하여 데이터 수집을 진행하였다.
 * 사이트로부터 7,259개의 판례 원문 데이터를 수집하였다.
 * 사이트에서 총 10가지의 마약의 키워드를 검색하여 판례 원문 데이터를 수집하였다.
 * 형량이 명시된 1심 판례에 한해 데이터 수집을 진행하였다.
 
 ### 2. 데이터 전처리
 * 서비스를 구현을 위해 판례 원문으로부터 다음 5가지 특징을 추출하였다.
 1) 사건번호: 판례 고유 번호
 2) 취급마약: 판례가 어떤 마약에 관한 판례인지를 나타냄. 
 3) 형종: 형량의 종류
 4) 형량범위: 형량의 범위
 5) 범죄사실: 선고에 적용된 범죄사실을 나타냄.
 * 전처리를 완료한 테이블은 다음과 같다.
 <img width="1280" alt="데이터 테이블" src="https://user-images.githubusercontent.com/121072239/212743274-4c37842c-075f-47cd-ac03-1db76795afc0.png">
 *  데이터 전처리에 관한 자세한 내용은 preprocessing.ipynb 파일을 참고

 ### 3. 서비스 구현
 * 서비스는 웹사이트 형태로 구현하였으며, Django 프레임워크를 사용해 구현하였다.
 * 본 서비스는 정식으로 배포되지 않았기 때문에, 로컬 서버에서만 구동이 가능하다.
 * 구동 방법은 다음과 같다.
 1) 개발환경에 맞는 가상환경을 실행한다.
 2) 터미널 경로를 myweb 폴더로 변경한다.
 3) 터미널에서 python manage.py runserver 명령을 실행한다.
 4) 브라우저를 통해 출력된 로컬 서버로 접속한다.

 ### 4. 서비스 주요 기능
 * 사이트 내 존재하는 판례 데이터의 마약별 분포를 조회한다.
 * 사용자가 선택한 마약에 따라 데이터 베이스 내 만족하는 데이터를 검색한다(데이터 베이스는 앞선 전처리 과정에서 생성한 data.csv 파일을 사용하였다).
 * 사용자의 입력값에 따라 판례 데이터의 형종별, 형량별 분포를 조회한다.
 * 사용자의 입력값에 따라 분포에 해당하는 판례 원문을 조회한다.
 * 서비스 주요 기능에 관한 자세한 내용은 views.py 파일을 참고

## 결과
* 구현한 서비스의 모습은 다음과 같다.
<img width="1280" alt="홈페이지" src="https://user-images.githubusercontent.com/121072239/212744318-0e3de277-1ffc-4ba4-a420-7c4439d69321.png">
<img width="1280" alt="마약별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/212744338-f012459f-af74-4457-b5f9-4107ced234ce.png">
<img width="1280" alt="검색 페이지" src="https://user-images.githubusercontent.com/121072239/212744346-00b07e0d-6298-4c1e-8a53-9713f74045b3.png">
<img width="1280" alt="형종별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/212744355-79a4311a-68d7-4dea-a03a-ece565746ad7.png">
<img width="1280" alt="형량별 데이터 분포 페이지" src="https://user-images.githubusercontent.com/121072239/212744369-569db9d4-086d-4d1b-9ac6-3af8d2cbb36a.png">
<img width="1280" alt="판례 원문 페이지" src="https://user-images.githubusercontent.com/121072239/212744374-a60cfba9-4b7c-4331-a9f4-081c8ecb02f4.png">

