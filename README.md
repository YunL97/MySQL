# MySQL

* 데이터 베이스란:
  *  데이터컬렉션이다.
  *  엑세스 가능한 인터페이스를 가진 컴퓨터화된 데이터의 구조화된 집합이다

* SQL: 구조화 쿼리언어(Structured Query Language)
  * 데이터베이스에게 말을걸 때 사용하는 언어
* sql코드는 RDBMS에서는 다 같다
* sql을 학습하고 나면 sql을 사용하는 다른 데이터베이스로 전환하는것이 크게 어렵지 않다
* 데이터베이스 관리 시스텝을 고유하게 만드는 것은 이것들이 제공하는 기능 이다 


# 데이터베이스, 테이블

* use `<database>;` 를통해 데이터베이스 변경 가능
* INT: 아주 큰  숫자를 다루는 경우가 아니라면 최댓값에 신경쓸 필요는 없다
* select database(); 를 통해 현재 사용하는 db 이름을 알 수 있다
* show tables;
* show columns from cats; == desc cats;
* 작은따옴표로 쿼리짜는게 좋다 큰따옴표 쓰면 얘기치 못한 오류가 나올 수 있음
* primary key: 필수일뿐만 아니라 고유해아한다. 식별자임
* cat_id INT NOT NULL PRIMARY KEY === PRIMARY KEY(cat_id)
* 프라이머리키는 자동으로 not null
* cat_id INT AUTO_INCREMENT: 자동 증가
*  