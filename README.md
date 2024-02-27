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
* Aliases: select cat_id AS id, name From cats;, 열의 이름을 다시 정해서 짧게 만들거나 쉽게 만들수 있다
* update employees set last_name='asdasd';
* 업데이트를 할때는 주의해줘야한다. 업데이트를 하기 전에는 select로 확인을 해봐야한다
* delete from cats where cat_id=age;
  

# 문자열
* concat: sellect concat('a', 'b', 'c');  -> abc
* concat 는 실제 데이터를 작업할때 유용 
* select concat(author, ' ', author_b) from books;
* substring: 긴 문자열을 취해서 작은 문자열로 반환하는 함수
* select concat(substr(title, 1, 10), '...') from books;
* replace: 문자열 일부를 다른 대체 문자열로 바꾼다
* reverse: 거꾸로 출력
* char_length: 길이
* length: 바이트길이

# 정교화
* distinct: 중복결과 제거
* order by asdf desc: 정렬 , asce(오름 차순)
* limit: 결과수 조절
* like: where author_fname like '%da%';, '_' _ 한개당 하나의 문자 

# 집계함수
* count: select count(*) from books where title like '%the%';
* group by: 같은거로 묶기, select author_name, count(*) from books group by author_name
* min, max
* 하위커리: select * from books where pages = (select min(pages) from books);
* sum: 더하기
* avg: 평균