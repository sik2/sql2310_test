# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
1. 서비스는 게시판, 회원 기능이 있다.
2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
# 1. 서비스는 게시판, 회원 기능이 있다.
# 2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
# 3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
# 4. 게시판 테이블과 회원 테이블은 1 : N 관계이다. 
# -> 정규화가 되어있음 게시판에 있는 id와 회원 table 정보가 여러개 들어잇고 연결되어있음
# 5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 

### 테이블 생성 sql
DROP DATABASE a1;
CREATE DATABASE a1;
USE a1;
### 테이블에 각각 테스트 데이터 2개씩 넣는 sql
CREATE TABLE article (
id int(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
name char(100) NOT NULL,
regDate datetime NOT NULL,
body text NOT NULL
);
INSERT INTO article
SET regDate = now(),
name = '홍길동',
body = '첫번째';

INSERT INTO article
SET regDate = now(),
name = '홍길순',
body = '두번째';
SELECT * FROM article;

CREATE TABLE members (
id int(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
name char(100) NOT NULL,
passw char (100) NOT NULL,
email char (100) NOT NULL
);

INSERT INTO members
SET name = '홍길동',
passw = '0000',
email =  '1234';

INSERT INTO members
SET name = '홍길순',
passw = '1111'
email =  '5678';

### 각 테이블을 JOIN 을 통하여 합치는 sql
SELECT M.id AS 번호,
M.name AS 작성자,
M.passw AS 비밀번호,
M.email AS 이메일
FROM members AS M
INNER JOIN article AS A
ON M.id = A.id;
### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql
INSERT INTO article
SET regDate = now(),
name = '비회원',
body = '세번째';

SELECT M.id AS 번호,
M.name AS 작성자,
M.passw AS 비밀번호,
M.email AS 이메일
FROM article AS A
left JOIN members AS M
ON M.name = A.name;



