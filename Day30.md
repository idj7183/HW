# Day30 HW
## 숙제 1
```
MariaDB [studydb]> SELECT * FROM pokemon;
+----+----------+-------+------------+
| no | name     | level | regdate    |
+----+----------+-------+------------+
|  1 | 피카츄   |     1 | 2020-05-05 |
|  2 | 라이츄   |     3 | 2020-01-01 |
|  3 | 파이리   |     5 | 2019-11-11 |
|  4 | 꼬부기   |     7 | 2019-05-05 |
|  5 | 리자몽   |    10 | 2019-01-01 |
|  6 | 이상해씨 |     1 | 2019-01-01 |
+----+----------+-------+------------+
6 rows in set (0.000 sec)

////// 1. 이름이 '피'로 시작하는 포켓몬들의 이름, 레벨 알려줘 (유사검색)
MariaDB [studydb]> SELECT name,level FROM pokemon WHERE name LIKE '피%';
+--------+-------+
| name   | level |
+--------+-------+
| 피카츄 |     1 |
+--------+-------+
1 row in set (0.001 sec)

////// 2. 등록일자가 2020/01/01 이전인 포켓몬들의 번호, 이름, 등록일자 알려줘
MariaDB [studydb]> SELECT no,name,regdate FROM pokemon WHERE regdate<STR_TO_DATE('20200101','%Y%m%d');
+----+----------+------------+
| no | name     | regdate    |
+----+----------+------------+
|  3 | 파이리   | 2019-11-11 |
|  4 | 꼬부기   | 2019-05-05 |
|  5 | 리자몽   | 2019-01-01 |
|  6 | 이상해씨 | 2019-01-01 |
+----+----------+------------+
4 rows in set (0.001 sec)

////// 3. 레벨이 5 이상 10 이하인 포켓몬들의 모든 정보 알려줘 
MariaDB [studydb]> SELECT * FROM pokemon WHERE level>=5 AND level<=10;
+----+--------+-------+------------+
| no | name   | level | regdate    |
+----+--------+-------+------------+
|  3 | 파이리 |     5 | 2019-11-11 |
|  4 | 꼬부기 |     7 | 2019-05-05 |
|  5 | 리자몽 |    10 | 2019-01-01 |
+----+--------+-------+------------+
3 rows in set (0.000 sec)

////// 4. 모든 포켓몬들의 레벨 보여줘 
MariaDB [studydb]> SELECT level FROM pokemon
    -> ;
+-------+
| level |
+-------+
|     1 |
|     3 |
|     5 |
|     7 |
|    10 |
|     1 |
+-------+
6 rows in set (0.000 sec)

////// 5. 모든 포켓몬들의 레벨 보여줘. 중복 제거 해줘.
MariaDB [studydb]> SELECT DISTINCT level FROM pokemon;
+-------+
| level |
+-------+
|     1 |
|     3 |
|     5 |
|     7 |
|    10 |
+-------+
5 rows in set (0.000 sec)

////// 6. 모든 포켓몬들의 이름, 레벨 보여줘. 이름 오름차순으로 보여줘
MariaDB [studydb]> SELECT name,level FROM pokemon ORDER BY name ASC;
+----------+-------+
| name     | level |
+----------+-------+
| 꼬부기   |     7 |
| 라이츄   |     3 |
| 리자몽   |    10 |
| 이상해씨 |     1 |
| 파이리   |     5 |
| 피카츄   |     1 |
+----------+-------+
6 rows in set (0.003 sec)

////// 7. 모든 포켓몬들의 이름, 레벨 보여줘. 레벨 많은 순으로 보여줘
MariaDB [studydb]> SELECT name,level FROM pokemon ORDER BY level DESC;
+----------+-------+
| name     | level |
+----------+-------+
| 리자몽   |    10 |
| 꼬부기   |     7 |
| 파이리   |     5 |
| 라이츄   |     3 |
| 피카츄   |     1 |
| 이상해씨 |     1 |
+----------+-------+
6 rows in set (0.001 sec)

////// 8. 모든 포켓몬들의 이름, 레벨 보여줘. 레벨 많은 순으로 보여줘, 같은 레벨이면 이름 오름차순으로 보여줘
MariaDB [studydb]> SELECT name,level FROM pokemon ORDER BY level DESC, name ASC;
+----------+-------+
| name     | level |
+----------+-------+
| 리자몽   |    10 |
| 꼬부기   |     7 |
| 파이리   |     5 |
| 라이츄   |     3 |
| 이상해씨 |     1 |
| 피카츄   |     1 |
+----------+-------+
6 rows in set (0.001 sec)

////// 9. 모든 포켓몬들의 이름, 레벨 보여줘. 등록일자 최신순으로 보여줘.
MariaDB [studydb]> SELECT name,level FROM pokemon ORDER BY regdate DESC;
+----------+-------+
| name     | level |
+----------+-------+
| 피카츄   |     1 |
| 라이츄   |     3 |
| 파이리   |     5 |
| 꼬부기   |     7 |
| 리자몽   |    10 |
| 이상해씨 |     1 |
+----------+-------+
6 rows in set (0.001 sec)
```
