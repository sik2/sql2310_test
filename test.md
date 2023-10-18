# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
# 1. 서비스는 게시판, 회원 기능이 있다.
# 2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
# 3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
# 4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
# 5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 


### 테이블 생성 sql
CREATE DATABASE 게시판;
USE 게시판;
CREATE TABLE 게시판(
	id int UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
	title VARCHAR(100) NOT NULL,
	body TEXT NOT NULL,
	regDate DATETIME NOT NULL,
	userName CHAR(100) NOT NULL UNIQUE
);

SELECT * FROM 게시판;

CREATE TABLE 회원(
	id int UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
	userName CHAR(100) NOT NULL UNIQUE,
	`password` CHAR(100) NOT NULL,
	email CHAR(100) NOT NULL UNIQUE
);

SELECT * FROM 회원;

### 테이블에 각각 테스트 데이터 2개씩 넣는 sql
### 게시판
USE 게시판;

SELECT * FROM 게시판;

INSERT INTO 게시판
SET title = '안녕하세요!',
body = '잘부탁드려요.',
regDate = now(),
userName = '홍길동'
;

INSERT INTO 게시판
SET title = '안녕히계세요!',
body = '다음에 또봐요.',
regDate = now(),
userName = '홍길순'
;

INSERT INTO 게시판
SET title = '비회원입니다.',
body = '안녕하세요',
regDate = now(),
userName = '비회원'
;

SELECT userName FROM 게시판;

###회원
# 3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
SELECT * FROM 회원;

INSERT INTO 회원
SET userName = '홍길동',
`password` = 'password1',
email = 'Hong-gil-dong@gmail.com'
;

INSERT INTO 회원
SET userName = '홍길순',
`password` = 'password2',
email = 'Hong-gil-sun@gmail.com'
;

### 각 테이블을 JOIN 을 통하여 합치는 sql
SELECT B.id AS 게시물ID, B.title AS 제목, B.body AS 내용, B.regDate AS 작성일,
       A.`password` AS 비밀번호, A.email AS 이메일
FROM 게시판 AS B
INNER JOIN 회원 AS A
ON B.userName = A.userName;

### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql
SELECT B.id AS 게시물ID, B.title AS 제목, B.body AS 내용, B.regDate AS 작성일,
       A.`password` AS 비밀번호, A.email AS 이메일
FROM 게시판 AS B
LEFT JOIN 회원 AS A
ON B.userName = A.userName;
