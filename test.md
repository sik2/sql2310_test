# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.
DROP DATABASE a1;
CREATE DATABASE a1;
use a1;
# 조건
#1. 서비스는 게시판, 회원 기능이 있다.
#2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
CREATE TABLE article(
id INT(10) UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
title VARCHAR(100) NOT NULL,
body TEXT NOT NULL,
regDate DATETIME NOT NULL
);

#3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
CREATE TABLE user(
id INT(10) UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
name CHAR(30) NOT NULL,
password INT(10) UNSIGNED NOT NULL,
email CHAR(30) NOT NULL,
articleID INT(10) NOT NULL
);

SELECT * FROM article;
SELECT * FROM user;

#4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
#5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 

### 테이블 생성 sql
SELECT * FROM article;
SELECT * FROM user;

### 테이블에 각각 테스트 데이터 2개씩 넣는 sql
INSERT INTO article
SET title = '제목1',
body = '내용1',
regDate = now();

INSERT INTO article
SET title = '제목2',
body = '내용2',
regDate = now();

INSERT INTO user
SET name = '홍길동',
password = 1234,
email = '네이버',
articleId = 1;

INSERT INTO user
SET name = '홍길순',
password = 5678,
email = '다음',
articleId = 2;


### 각 테이블을 JOIN 을 통하여 합치는 sql
SELECT U.name AS '작성자',
DATE(A.regDate) AS '작성일자',
A.title AS '글 제목',
A.body AS '글 내용',
U.email AS '이메일',
U.password AS '비밀번호'
FROM user AS U
INNER JOIN article AS A
ON U.id = A.id


### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql
INSERT INTO article
SET title = '제목3',
body =  '내용3',
regDate = NOW();

SELECT U.name AS '작성자',
DATE(A.regDate) AS '작성일자',
A.title AS '글 제목',
A.body AS '글 내용',
U.email AS '이메일',
U.password AS '비밀번호'
FROM article AS A
LEFT JOIN user AS U
ON A.id = U.articleId;
