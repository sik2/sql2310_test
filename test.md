# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
1. 서비스는 게시판, 회원 기능이 있다.
2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 
### 테이블 생성 sql
DROP DATABASE IF EXISTS service;
CREATE DATABASE service;
USE service;


CREATE TABLE `member`(
id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
loginId CHAR(50) NOT NULL,
loginPw VARCHAR(100) NOT NULL,
mail CHAR(100) NOT NULL
)

CREATE TABLE post (
id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
postId CHAR(100) NOT NULL,
post NOT NULL,
regDate DATETIME NOT NULL,
poster_loginId INT
)


### 테이블에 각각 테스트 데이터 2개씩 넣는 sql


### 각 테이블을 JOIN 을 통하여 합치는 sql

### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql



