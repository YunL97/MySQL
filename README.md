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

# 데이터 유형

* char: 길이 고정, asd char(2)-> 크기가 고정 3이상은 안들어감, 문자 한개 넣어도 2byte 고정, 길이가 고정된거에 사용하는게 좋음
* decimal: int를 사용하면 소수점 뒤자리는 모두 제거한다, decimal을 사용하면 정확한 소수 저장가능
* 메모리에 소수를 저장하는것은 까다로운 작업 decimal(5,2) -> 999.99
* float, double로 출분하다
* date: 날짜저장, 시간포함x yyyy-mm-dd, curdate
* time: 시간저장, hh:mm:ss, curtime
* datetime: yyyy-mm-dd hh:mm:ss, now
* day(2024-02-27): 무슨요일인지 알려줌
* date_format: 날짜양식 변경 select date_format(asd, '%a %b) from people;
* datediff: 날짜 계산 select datediff('2010-11-30', '2010-12-31') -> 31
* timestamps: timestamps로 저장하면 효율적이고 공간을 덜차지, 특정 이벤트가 발생한 시점을 기록하거나 레코드의 마지막 업데이트 시간을 측정하는데 사용, 서버의 시간대 설정에 따라 변환되고 자동업데이트 된다
  
# 논리연산자

* not equal: select * from asd where a != 'aaa';
* not like: like 반대
* greater than: ~보다 크다
* between: where year between 2004 and 2014;
* cast: 데이터 유형을 다른 데이터 유형으로 변환해준다
  *  where birth between cast('12:00:00' as time) and cast('16:00:00' as time);
* in: 포함된거를 찾는것 or 겹치면 안좋기 때문 where author in ('lee', 'kim','sun');
* not in: in 반대
* then: 
  * select a, case when year > 2000 then 'asd' else 'cc' end from books;
* where null 사용할때는 =null 말고 where title is null

# 제약조건
* constraint
* unique: phone varchar(10) not null unique, 중복 방지가능
* check: age int check (age > 18)

# 테이블변경
* 열추가: alter table a add column b int not null;
* 열삭제: alter table a drop column b;
* 테이블 이름변경: rename table a to c;
* 열 이름 변경: rename column b to c;
* 열 수정 alter table c modiy b varchar(100);

# 일대일, 일대다, 다대다
* 조인, 외래키 기본키, 일대일, 일대다, 다대다
* 일대다: 다대다에 비해 다루기 쉽고 짧을뿐만 아니라 개발에서 가장 널리 사용되고 중심이 된다
* 외래키: 어떤 테이블 안에 있는 다른 테이블을 참조하는 것
```
create table orders (
  customer_id int,
  foregin key (customer_id) references customers(id)
)
```
* inner join: 교집합
```
select * from customers 
join orders on orders.customer_id = customers.id
```
* left join: 왼쪽인데, 왼쪽 테이블 한개의 레코드에 여려개 오른쪽 레코드가 일치할 경우 왼쪽을 여러번 표시, 왼쪽은 무조건 표시하고, 매치되는거 없으면 null
* right join: 왼족 반대
* cascade: 외래키 사용시 그 데이터를 지우면 안지워지는데 cascade 사용하면 그 데이터를 지우면 외래키가 포함된 데이터를 삭제할 수 있다
```
foregin key (customer_id) references customers(id) on delete cascade
```

# 다대다 
* ex) 책에 많은 저자가 있는경우, 작가들에게 많은 책이 있는 경우

# 다양한기능
* 뷰: 저장된 쿼리로 호출시 결과집합을 생성, 뷰는 가상 테이블의 역할을 한다
* 뷰는 늘 모든 ㅔ이블 작업이 가능한 실제 테이블처럼 취급이 안된다. 삭제, 업데이트, 삽입등의 테이블 작업이 가능한건 일부에 불과하다
* having: group by 로 얻은 그룹을 필터링하는데 사용된다
```
select title, avg(rating) from asd
group by title having count(rating) > 1 
```

# 윈도우함수
* 행과 행 간의 관계정의, 순위, 합계, 평군, 행위치 등을조작, group by 구문과 병행하여 사용하지 않을때 사용