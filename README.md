# javamukja 팀 프로젝트입니다.
요리에 대한 토론과 레시피 공유등을 위한 목적으로 만들어졌습니다.
Spring Framework MVC 패턴으로 만들었고 사용한 데이터베이스는 Oracle DB 입니다.


[JAVAMUKJA Project 기초 테이블]
DROP TABLE member CASCADE CONSTRAINTS;
DROP TABLE grade CASCADE CONSTRAINTS;
DROP TABLE recipe CASCADE CONSTRAINTS;
DROP TABLE find CASCADE CONSTRAINTS;
DROP TABLE notice CASCADE CONSTRAINTS;
DROP TABLE talk CASCADE CONSTRAINTS;
DROP TABLE gradereply CASCADE CONSTRAINTS;
DROP TABLE recipereply CASCADE CONSTRAINTS;
DROP TABLE talkreply CASCADE CONSTRAINTS;
select * from tab;
CREATE TABLE member (
       id                   varchar(20) NOT NULL,
       mname                varchar(20) NOT NULL,
       passwd               varchar(20) NOT NULL,
       fname                varchar(50) NOT NULL,
       email                varchar(50) NOT NULL,
       nickname             varchar(20) NOT NULL,
       grade                CHAR(1) DEFAULT 'N' NOT NULL
                                   CHECK (grade IN ('A', 'C', 'N')),
       address              varchar(150) NULL,
       zipcode              varchar(7) NULL,
       PRIMARY KEY (id)
);


CREATE TABLE grade (
       gno                  number(7) NOT NULL,
       id                   varchar(20) NOT NULL,
       title                varchar(100) NOT NULL,
       content              varchar(4000) NOT NULL,
       rdate                date NOT NULL,
       PRIMARY KEY (gno), 
       FOREIGN KEY (id)
                             REFERENCES member
);


CREATE TABLE gradereply (
       grno                 number(7) NOT NULL,
       id                   varchar(20) NOT NULL,
       gno                  number(7) NOT NULL,
       rdate                date NOT NULL,
       content              varchar(2000) NOT NULL,
       PRIMARY KEY (grno), 
       FOREIGN KEY (id)
                             REFERENCES member, 
       FOREIGN KEY (gno)
                             REFERENCES grade
);


CREATE TABLE find (
       fno                  number(7) NOT NULL,
       fstr                 varchar(60) NOT NULL,
       fcnt                 number(5) DEFAULT 0 NOT NULL,
       fdate                date NOT NULL,
       PRIMARY KEY (fno)
);


CREATE TABLE recipe (
       rno                  number(7) NOT NULL,
       id                   varchar(20) NOT NULL,
       title                varchar(100) NOT NULL,
       content              varchar(4000) NOT NULL,
       viewcnt              number(5) DEFAULT 0 NOT NULL,
       rcnt                 number(5) DEFAULT 0 NOT NULL,
       fname                varchar(50) NULL,
       category             varchar(50) NOT NULL,
       time                 varchar(20) NOT NULL,
       portion              varchar(20) NOT NULL,
       ingredient           varchar(1000) NOT NULL,
       rdate                date NOT NULL,
       PRIMARY KEY (rno), 
       FOREIGN KEY (id)
                             REFERENCES member
);


CREATE TABLE recipereply (
       rrno                 number(7) NOT NULL,
       id                   varchar(20) NOT NULL,
       rno                  number(7) NOT NULL,
       rdate                DATE NOT NULL,
       content              varchar(2000) NOT NULL,
       PRIMARY KEY (rrno), 
       FOREIGN KEY (id)
                             REFERENCES member, 
       FOREIGN KEY (rno)
                             REFERENCES recipe
);


CREATE TABLE notice (
       nno                  number(7) DEFAULT 0 NOT NULL,
       id                   varchar(20) NOT NULL,
       title                varchar(100) NOT NULL,
       content              varchar(4000) NOT NULL,
       viewcnt              number(5) DEFAULT 0 NOT NULL,
       category             varchar(50) NOT NULL,
       rdate                date NOT NULL,
       PRIMARY KEY (nno), 
       FOREIGN KEY (id)
                             REFERENCES member
);



CREATE TABLE talk (
       tno                  number(7) NOT NULL,
       id                   varchar(20) NOT NULL,
       title                varchar(100) NOT NULL,
       content              varchar(4000) NOT NULL,
       viewcnt              number(5) DEFAULT 0 NOT NULL,
       rcnt                 number(5) DEFAULT 0 NOT NULL,
       fname                varchar(50) NULL,
       hashtag              varchar(100) NOT NULL,
       category             varchar(50) NOT NULL,
       rdate                DATE NOT NULL,
       PRIMARY KEY (tno), 
       FOREIGN KEY (id)
                             REFERENCES member
);

CREATE TABLE talkreply (
       trno                 number(7) NOT NULL,
       id                   varchar(20) NOT NULL,
       tno                  number(7) NOT NULL,
       rdate                date NOT NULL,
       content              varchar(2000) NOT NULL,
       PRIMARY KEY (trno), 
       FOREIGN KEY (id)
                             REFERENCES member, 
       FOREIGN KEY (tno)
                             REFERENCES talk
);

insert into member(id, mname, passwd, fname, email, nickname, address, zipcode, grade)
values('admin', '관리자', '1234', 'man.jpg', 'admin@admin.com', '관리자',
'서울시 종로구', '101-123', 'A');

insert into member(id, mname, passwd, fname, email, nickname, address, zipcode, grade)
values('chef', '셰프', '1234', 'man.jpg', 'chef@chef.com4', '셰프',
'서울시 종로구', '101-123', 'C');

insert into member(id, mname, passwd, fname, email, nickname, address, zipcode, grade)
values('user1', '홍길동', '1234', 'man.jpg', 'user1@user1.com', '홍길동',
'서울시 종로구', '101-123', 'N');





