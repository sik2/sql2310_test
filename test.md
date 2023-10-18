# 아래 조건에 맞게 테이블을 구성하는 sql 문법을 작성하여 제출하시오.

# 조건
# 1. 서비스는 게시판, 회원 기능이 있다.
# 2. 게시판의 경우 게시글 이름, 내용, 생성일, 작성자 로 구성 되어 있다.
# 3. 회원의 경우 이름, 비밀번호, 이메일로 구성이 되어있다.
# 4. 게시판 테이블과 회원 테이블은 1 : N 관계이다.
# 5. 각 테이블의 id 값은 고유해야하며, 비어있으면 안된다.

## 제출 

### 테이블 생성 sql
CREATE TABLE board(
	id INT UNSIGNED AUTO_INCREMENT NOT NULL,
	PRIMARY KEY(id),
	title CHAR(100) NOT NULL,
	content CHAR(100) NOT NULL,
	regDate DATETIME NOT NULL,
	writer CHAR(100) NOT NULL
);

CREATE TABLE `member`(
	id INT UNSIGNED AUTO_INCREMENT NOT NULL,
	PRIMARY KEY(id),
	name CHAR(100) NOT NULL,
	`password` INT NOT NULL,
	email CHAR(100) NOT NULL
);

### 테이블에 각각 테스트 데이터 2개씩 넣는 sql
INSERT INTO board
SET title = "테스트 제목입니다1.",
content = "테스트 내용입니다1.",
regDate = now(),
writer = "홍길동";

INSERT INTO board
SET title = "테스트 제목입니다2.",
content = "테스트 내용입니다2.",
regDate = now(),
writer = "길동무";

INSERT INTO `member`
SET name = "홍길동",
`password` = 123456,
email = "test1@naver.com";

INSERT INTO member
SET name = "길동무",
`password` = 123456,
email = "test2@naver.com";

### 각 테이블을 JOIN 을 통하여 합치는 sql
SELECT * FROM board
INNER JOIN `member`
ON board.writer = `member`.name; 

### 비회원으로 작성된 (게시글 테이블의 회원 id가 없는 경우) 케이스를 추가하고 이를 left join 을 통해서 출력하는sql
INSERT INTO board
SET title = "테스트 제목입니다3.",
content = "테스트 내용입니다3.",
regDate = now(),
writer = "비회원";

SELECT * FROM board
LEFT JOIN `member`
ON board.writer = `member`.name; 
