# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
#1. 서비스는 게시판, 회원 기능이 있다.
#2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
#3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
#4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
#5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 

### 테이블 생성 sql
CREATE DATABASE a5;
USE a5;

CREATE TABLE board(
id int(10) UNSIGNED NOT NULL AUTO_INCREMENT,
PRIMARY KEY(id),
regDate DATETIME NOT NULL,
title CHAR(100) NOT NULL,
`text` TEXT NOT NULL,
memberId int(10) NOT NULL 
);


CREATE TABLE `member`(
id int(10) UNSIGNED NOT NULL AUTO_INCREMENT,
PRIMARY KEY(id),
name CHAR(100) NOT NULL,
`password` TEXT NOT NULL UNIQUE,
userEmail TEXT NOT NULL UNIQUE
);

DROP TABLE board;
DESC board;
SELECT *  FROM board;

SELECT * FROM `member`;	


### 테이블에 각각 테스트 데이터 2개씩 넣는 sql

INSERT INTO board
SET regDate = NOW(),
	title = '질문',
	`text` = '질문있습니다.',
	memberId = 1;



INSERT INTO board
SET regDate = NOW(),
	title = '대답',
	`text` = '대답입니다.',
	memberId = 2;

INSERT INTO `member`
SET name = '홍길동',
	`password` = 'ghdrlf',
	userEmail = 'ghdrlfehd@gmail.com';

INSERT INTO `member`
SET name = '홍길순',
	`passWord` = 'rlftns',
	userEmail = 'ghdrlftns@gmail.com';
	
	

### 각 테이블을 JOIN 을 통하여 합치는 sql

SELECT 
B.title, 
M.name, 
M.userEmail
FROM board AS B
JOIN `member` AS M
ON B.memberId = M.id;

### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql
SELECT * FROM board;
SELECT * FROM `member`;

INSERT INTO board 
SET regDate = NOW(),
	title = '의문점',
	`text` = '궁금합니다.',
	memberId = 0;
	
SELECT 
B.title, 
ifnull(M.name, '비회원') AS 회원명,
IF(M.userEmail IS NOT NULL, M.userEmail, '비회원') AS email
FROM board AS B
LEFT JOIN `member` AS M
ON B.memberId = M.id;
