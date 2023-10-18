# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
# 1. 서비스는 게시판, 회원 기능이 있다.
# 2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
# 3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
# 4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
# 5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 
SELECT * FROM noticeBoard ;
SELECT * FROM `user` ;
DROP DATABASE service;
### 테이블 생성 sql
CREATE DATABASE service;
USE service;

CREATE TABLE noticeBoard(
id int(10) UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE PRIMARY KEY,
name text NOT NULL ,
content text NOT NULL,
regDate datetime NOT NULL,
writer text NOT NULL);

CREATE TABLE `user` (
id int(10) UNSIGNED NOT NULL AUTO_INCREMENT UNIQUE PRIMARY KEY,
name text NOT NULL,
`password` text NOT NULL,
email text NOT null
);

### 테이블에 각각 테스트 데이터 2개씩 넣는 sql
INSERT INTO `user`
SET name = '홍길동',
`password` = '1234',
eMail = '123@123.123';

INSERT INTO `user`
SET name = '홍길순',
`password` = '1234',
eMail = '1234@1234.1234';

INSERT INTO noticeBoard 
SET name = '안녕하세요~',
content = '오늘 가입했어요~',
regDate = now(),
writer = '홍길동';

INSERT INTO noticeBoard 
SET name = '안녕하십니까',
content = '오늘 가입했습니다.',
regDate = now(),
writer = '홍길순';

### 각 테이블을 JOIN 을 통하여 합치는  <회원이 작성한 글 보기(부서에 속해있는 사람들 보기)>
SELECT U.name AS 유저명, NB.name AS 작성글, NB.content AS 내용 FROM `user` AS U
JOIN noticeBoard AS NB ON U.name = NB.writer;

#글쓴이가 어떤사람인지 보기(사원이 어느부서에 속해있는지 보기)
SELECT U.name AS 유저명, NB.name AS 작성글, NB.content AS 내용 FROM noticeBoard AS NB
JOIN `user` AS U ON  NB.writer = U.name;

### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql
INSERT INTO noticeBoard 
SET name = '비회원 글쓰기',
content = '비회원이 쓴 글',
regDate = NOW(),
writer = 0;

SELECT * FROM noticeBoard ;


# 
SELECT U.name AS 유저명, NB.name AS 작성글, NB.content AS 내용 FROM noticeBoard AS NB
LEFT JOIN `user` AS U ON  NB.writer = U.name;


