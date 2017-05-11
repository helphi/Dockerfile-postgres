postgres chinese search support

Tag | Dockerfile | Image Layers
----|------------|-------------
`9.4` | [Dockerfile](https://github.com/helphi/Dockerfile-postgres-zhparser/blob/master/9.4/Dockerfile) | [![](https://images.microbadger.com/badges/image/helphi/postgres-zhparser:9.4.svg)](https://microbadger.com/images/helphi/postgres-zhparser:9.4 "Get your own image badge on microbadger.com")

## settings

### change default search config and restart postgresql

```sh
sed -i "s/pg_catalog.english/simple_zh_cfg/g" postgresql.conf
```

### config your database with zhparser

```sh
psql -Upostgres postgres -c 'CREATE EXTENSION zhparser'
psql -Upostgres postgres -c 'CREATE TEXT SEARCH CONFIGURATION simple_zh_cfg (PARSER = zhparser);'
psql -Upostgres postgres -c 'ALTER TEXT SEARCH CONFIGURATION simple_zh_cfg ADD MAPPING FOR n,v,a,i,e,l WITH simple;'
```

> NOTE: replace db name `postgres` with your db name
