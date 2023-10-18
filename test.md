# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
-- 1. 서비스는 게시판, 회원 기능이 있다.
-- 2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
-- 3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
-- 4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
-- 5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 

### 테이블 생성 sql
CREATE DATABASE a1;

USE a1;

DROP TABLE board;

CREATE TABLE writer (
name CHAR(100) NOT NULL,
`pasword` INT UNSIGNED NOT NULL,
email CHAR(100) NOT NULL,
id INT UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE,
writerid INT UNSIGNED NOT NULL,
PRIMARY KEY(id)
);

CREATE TABLE board (
name CHAR(100) NOT NULL,
content CHAR(100) NOT NULL,
regDate DATETIME NOT NULL,
creatName CHAR(100) NOT NULL,
id INT UNSIGNED NOT NULL AUTO_INCREMENT,
PRIMARY KEY(id)
);

DROP TABLE board;

DROP TABLE writer;


### 테이블에 각각 테스트 데이터 2개씩 넣는 sql

INSERT INTO writer 
SET name = '글쓴이홍길순',
`pasword` = 1111,
email = 'hong@naver.com',
writerid = 1;

INSERT INTO writer 
SET name = '글쓴이김배배',
`pasword` = 2222,
email = 'baebae@naver.com',
writerid = 2;

INSERT INTO board 
SET regDate = NOW(),
name = '소통게시판',
content = '우리 소통해요.!',
creatName = '작성자홍길동'
;

INSERT INTO board 
SET regDate = NOW(),
name = '사건사고게시판',
content = '사건사고를 해결해봐요.!',
creatName = '작성자김철수'
;

DESC board;

SELECT * FROM board;

SELECT * FROM writer;

### 각 테이블을 JOIN 을 통하여 합치는 sql

SELECT writer.name AS '작성자',
writer.`pasword` AS '비밀번호',
writer.email AS '주소',
writer.writerid AS '번호',
board.creatName AS '작성자명'
FROM writer
INNER JOIN board
ON board.id = writer.writerid;

### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql

INSERT INTO writer SET name = '비회원',  namePassword = 3333, email = 'noname@naver.com';

SELECT writer.name AS '작성자', writer.`pasword` AS '비밀번호', writer.email AS '주소명', board.name AS '게시판명'
FROM writer LEFT JOIN board
ON writer.id = board.id;

