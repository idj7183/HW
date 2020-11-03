# Day30 HW
```
MariaDB [studydb]> SELECT * FROM pokemon
    -> ;
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

MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
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

MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]>
MariaDB [studydb]> SELECT name,level FROM pokemon WHERE name LIKE '피%'
    -> ;
+--------+-------+
| name   | level |
+--------+-------+
| 피카츄 |     1 |
+--------+-------+
1 row in set (0.001 sec)

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

MariaDB [studydb]> SELECT * FROM pokemon WHERE level>=5 AND level<=10;
+----+--------+-------+------------+
| no | name   | level | regdate    |
+----+--------+-------+------------+
|  3 | 파이리 |     5 | 2019-11-11 |
|  4 | 꼬부기 |     7 | 2019-05-05 |
|  5 | 리자몽 |    10 | 2019-01-01 |
+----+--------+-------+------------+
3 rows in set (0.000 sec)

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
