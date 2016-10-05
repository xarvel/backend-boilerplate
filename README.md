# Backend Boilerplate

<img width="100%" src="/img/intro.png?raw=true">

Nginx, PHP7(+ Xdebug), PostgreSQL, Redis

Deploy database

```
docker cp dump.sql.gz database_container_name:/tmp/dump.sql.gz
docker exec -ti database_container_name bash
gunzip -c /tmp/dump.sql.gz | psql -U dbuser dbname
```

## About

* [valiullin.arthur@gmail.com](valiullin.arthur@gmail.com)