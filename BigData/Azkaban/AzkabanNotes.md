# Notes





### 配置MySQL

```
CREATE DATABASE azkaban;

CREATE USER 'azkaban'@'%' IDENTIFIED BY 'li123...';

GRANT SELECT,INSERT,UPDATE,DELETE ON azkaban.* to 'azkaban'@'%' WITH GRANT OPTION;

use azkaban;

source /opt/module/azkaban-3.84.4/azkaban-db-3.84.4/create-allsql-3.84.4.sql
```





```
bin/start-exec.sh

curl -G "l9z102:12321/executor?action=activate" && echo
curl -G "l9z103:12321/executor?action=activate" && echo
curl -G "l9z104:12321/executor?action=activate" && echo


bin/shutdown-exec.sh 
```













