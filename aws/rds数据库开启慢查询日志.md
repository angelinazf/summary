# aws上RDS数据开启慢查询日志

* 选择RDS->参数组，选择需要更改的参数组(注意：默认的参数组无法更改，需要新建一个参数组)
```
slow_query_log:要开启慢查询日志，请设置为1，默认为0
general_log:要开启一般日志，请设置为1，默认为0
long_query_time:只记录查询时间超过指定时间的sql，0.5代表只记录查询时间超过0.5s的sql语句
long_query_not_using_indexes:记录所有不使用索引的sql语句，即使未超过long_query_time也会记录
log_output: TABLE(默认):写到mysql.general_log以及mysql.slow_log表
            FILE(推荐):将一般查询日志和慢查询日志写到文件系统，每小时轮换一次
            NONE:禁用日志记录
```
* 启用了日志记录时，Amazon RDS 会定期轮换表日志或删除日志文件，log_output为TABLE时如需手动轮换执行：
```sql
CALL mysql.rds_rotate_slow_log;
CALL mysql.rds_rotate_general_log;
```
* log_output为FILE时会每小时检查日志文件并删除 24 小时之前的日志文件。

* 一般的实际应用参数
```
slow_query_log=1
general_log=1
long_query_time=0.5
log_queries_not_using_indexes=1
log_output=FILE
```