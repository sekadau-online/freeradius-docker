FROM freeradius/freeradius-server:3.0

RUN apt-get update && apt-get install -y freeradius-mysql mariadb-client && rm -rf /var/lib/apt/lists/*

COPY ./mods-config/sql/main/mysql/schema.sql /etc/freeradius/mods-config/sql/main/mysql/schema.sql
