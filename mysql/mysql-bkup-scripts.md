# mysql-bkup-scripts

mysql backup script:

```
# better to use $ENV_DB_USERNAME / $ENV_DB_PASSWORD
DB_USER=""							
DB_PASSWD=""						

DB_NAME="test"
TABLE_NAME="test_userasset"

FILEPATH="/MNT_Point/bkup/db-bkup/"
# 时间格式, %F 2019-05-09, %H_%M_%S 时分秒 09_32_55, %s ts格式 1557384286 
CURRENT_TIME=$(date +"%F_%H_%M_%S_%s")
FILENAME=db-bkup-${DB_NAME}-${TABLE_NAME}-${CURRENT_TIME}.sql
FULLNAME=${FILEPATH}${FILENAME}


bkup_db() {
	mysqldump -u$DB_USER -p$DB_PASSWD  ${DB_NAME} ${TABLE_NAME} > ${FULLNAME}
}

bkup_db
ls -l ${FULLNAME}
#echo ${CURRENT_TIME}
```



