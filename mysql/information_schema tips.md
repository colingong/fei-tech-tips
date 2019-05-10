# information_schema tips

```
select table_schema, table_name,data_length, index_length from information_schema.tables order by data_length desc limit 20 ;
```



对于Innodb，一个表里的数据全删掉，很可能仍然会占用很大的空间。而optimize table 会提示"Table does not support optimize, doing recreate + analyze instead"，而且占用的空间并不释放；运行"analyze table ..."可以把空间完全释放掉。

```
optimize table <table_name>
analyze table <table_name>
```



