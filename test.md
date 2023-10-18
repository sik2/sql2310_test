# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
# 1. 서비스는 게시판, 회원 기능이 있다.
# 2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
# 3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
# 4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
# 5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 

### 테이블 생성 sql
DROP DATABASE IF EXISTS a6;
CREATE DATABASE a6;
USE a6;
SHOW DATABASES;

CREATE TABLE board(
    id INT UNSIGNED PRIMARY KEY NOT NULL AUTO_INCREMENT,
    regDate DATETIME NOT NULL,
    boardName CHAR(100) NOT NULL,
    content VARCHAR(100) NOT NULL,
    writer CHAR(100) NOT NULL
);

SELECT * FROM board;


CREATE TABLE USER (
     id INT UNSIGNED PRIMARY KEY NOT NULL AUTO_INCREMENT,
     userName CHAR(100) NOT NULL,
     pass CHAR(100) NOT NULL,
     email CHAR(100) NOT NULL 
);

SELECT * FROM USER;
### 테이블에 각각 테스트 데이터 2개씩 넣는 sql
SELECT * FROM board;

INSERT INTO board
SET regDate = NOW(),
boardName = '첫째 게시판',
content = '내용1',
writer = '홍길동';

INSERT INTO board
SET regDate = NOW(),
boardName = '두번째 게시판',
content = '내용2',
writer = '임꺽정';

SELECT * FROM USER;
SELECT * FROM board;

INSERT INTO USER
SET userName = '홍길동',
pass = 'aa',
email = 'aaa';

INSERT INTO USER
SET userName = '임꺽정',
pass = 'bb',
email = 'bbb';

### 각 테이블을 JOIN 을 통하여 합치는 sql
SELECT *
FROM USER
JOIN board;

### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql
INSERT INTO board
SET regDate = NOW(),
boardName = '셋째 게시판',
content = '내용3',
writer = ' ';

SELECT B.content AS `게시판 내용`,
B.boardName AS '제목',
U.userName AS `회원 아이디`,
U.id AS `아이디`
FROM board AS B
LEFT JOIN USER AS U
ON B.writer = U.userName;





