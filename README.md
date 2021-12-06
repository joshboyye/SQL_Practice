# SQL_Practice


## DDL (Data Definition Language)

### Create TABLE
```
CREATE TABLE STADIUM (
STADIUM_ID    CHAR(3) NOT NULL,
STADIUM_NAME  VARCHAR2(40) NOT NULL,
HOMETEAM_ID   CHAR(3), /*char 캐릭터 입력*/
SEAT_COUNT    NUMBER,/*number */
ADDRESS       VARCHAR2(60), /*varchart string data type*/
DDD           VARCHAR2(3),
TEL           VARCHAR2(10),
CONSTRAINT STADIUM_PK PRIMARY KEY (STADIUM_ID) /*primary key 주민번호 처럼 제일 중유한 번호 */
);

CREATE TABLE TEAM ( 
TEAM_ID CHAR(3) NOT NULL, 
REGION_NAME VARCHAR2(8) NOT NULL,
TEAM_NAME VARCHAR2(40) NOT NULL, 
E_TEAM_NAME VARCHAR2(50), 
ORIG_YYYY CHAR(4), 
STADIUM_ID CHAR(3) NOT NULL,
ZIP_CODE1 CHAR(3), 
ZIP_CODE2 CHAR(3), 
ADDRESS VARCHAR2(80), 
DDD VARCHAR2(3),
TEL VARCHAR2(10), 
FAX VARCHAR2(10), 
HOMEPAGE VARCHAR2(50), 
OWNER VARCHAR2(10), 
CONSTRAINT TEAM_PK PRIMARY KEY (TEAM_ID),/*primary key */
CONSTRAINT TEAM_FK FOREIGN KEY (STADIUM_ID) /*references */REFERENCES STADIUM(STADIUM_ID) );

CREATE TABLE PLAYER ( 
PLAYER_ID CHAR(7) NOT NULL, 
PLAYER_NAME VARCHAR2(20) NOT NULL, 
TEAM_ID CHAR(3) NOT NULL, 
E_PLAYER_NAME VARCHAR2(40),
NICKNAME VARCHAR2(30), 
JOIN_YYYY CHAR(4), 
POSITION VARCHAR2(10), 
BACK_NO NUMBER(2),
NATION VARCHAR2(20), 
BIRTH_DATE DATE,
SOLAR CHAR(1), 
HEIGHT NUMBER(3), 
WEIGHT NUMBER(3), 
CONSTRAINT PLAYER_PK PRIMARY KEY (PLAYER_ID), 
CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID) );
```

## Modify TABLE
``` 
ALTER TABLE Stadium ADD /*add하나 테이블 더만들기*/

Test1 VARCHAR2(10) not null; /*not null 똑같은 번호나 이름 방지 하기 위해서*/

ALTER TABLE Stadium DROP COLUMN Test1;  

ALTER TABLE Stadium rename COLUMN Test1 to test2; /*rename 이름 바꾸기*/

ALTER TABLE Stadium MODIFY (Test1 VARCHAR2(10) not null);

ALTER TABLE PLAYER DROP CONSTRAINT PLAYER_FK;

ALTER TABLE PLAYER ADD CONSTRAINT PLAYER_FK2 FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID);

DROP TABLE Player2; /*drop테이블 전채삭제*/
RENAME player TO player2; /*rename 이름 바꾸기*/

TRUNCATE TABLE player; /*=Delete from Player;*/
``` 

## DML (Data Manipulation Language)

```
UPDATE PLAYER SET JOIN_YYYY = 2021 where Player_Id = 2009175;

update player set join_yyyy = 2021;

delete player where player_id = 2010112;

select p.player_name as players, p.player_id as id, p.join_YYYY as join 
from player p;

select * 
from player
where position = 'DF'
AND TEAM_ID = 'K04'
AND SOLAR = 2 
AND Weight <= 77;

select 컬럼 from 테이블 ;


문자형 함수
lower 
upper 
substr/substring 
length/len
LTRIM 
RTRIM
TRIM

숫자함수 
ABS
SIGN
MOD 
ROUND 
TRUND

CASE (if statement)
CASE 

```

## TCL (Data control language)
```
COMMIT; //데이터를 저장함 commit안하면 저장 안됌
rollback; /*한 데이터를delete한 다음 rollback를하면 그 데이터를 다시 대돌릴수있는 명령어*/
SAVEPOINT; /**/

```
## WHERE 절 
```
select*
from player(table name)
where Player_name like '이_';
% persent = 성이 이 시 인사람 다 조해 해보기
_ underline = 성 두글자나 이_ 옆에 있는 글자를 조회해보기s
 
select*
from player(table name)
where HEIGHT(ROW 에 있는 ID) = 180 

> more than 
>= more than equal
<less than 
<=less than equal 

"like" = 쓰는거
 
where HEIGHT between 170 and 180;
BETWEEN a AND b = a와 b의 값 사이에 있는거를 조회  /*ex. 키 170 에서 180 조회 where height between 170 and 180*/;

and //true and false 
or //true or true 
not 무조건 아닌것 조회 

!= not equal 같지 않다 


```
## GROUP BY, HAVING 절
```
group by // 테이블에 있는 id들 하고 avg를 사용한다음 id들을 정리를 해준다 

```

## ORDER BY 
```
order by // grouping up by using decending order or ascending order 
desc //descending order 
asc //ascending order

```
## JOIN 
```
player에 있는 테이블에 team 으로 join 하면 player 하고 team테이블 둘다 조회할수있다 

select *
from player p, team t
where p.height <170
and p.team_id = t.team_id;

select *
from player p inner join team t
on p.team_id = t.team_id;

```
