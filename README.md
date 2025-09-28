

#etc/freeradius/mods-available/sql

driver = "rlm_sql_mysql"
dialect = "mysql"

server = "db"
port = 3306
login = "radius"
password = "radiuspass"
radius_db = "radius"

pool {
    start = 5
    min = 4
    max = 10
    spare = 3
}
#aktivasi
ln -s /etc/freeradius/mods-available/sql /etc/freeradius/mods-enabled/sql
#build
docker compose up -d --build
#check log
docker logs -f freeradius_srv
#tambah user
docker exec -it radius_db mariadb -u radius -pradiuspass radius -e "
INSERT INTO radcheck (username, attribute, op, value)
VALUES ('fauzan', 'Cleartext-Password', ':=', '123456');"
#test auth
radtest fauzan 123456 localhost 0 testing123

