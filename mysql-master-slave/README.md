https://tarunlalwani.com/post/mysql-master-slave-using-docker/

```
$ docker-compose up -d
$ docker-compose logs -f mysqlconfigure
$ docker-compose exec mysqlmaster mysql -uroot -proot -e "CREATE DATABASE test_replication;"
$ docker-compose exec mysqlslave mysql -uroot -proot -e "SHOW DATABASES;"
```

```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test_replication   |
+--------------------+
```