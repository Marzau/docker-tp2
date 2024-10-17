FROM mysql:8.0

ENV MYSQL_ROOT_PASSWORD=rootpass
ENV MYSQL_DATABASE=testdb
ENV MYSQL_USER=user
ENV MYSQL_PASSWORD=userpass

COPY init.sql /docker-entrypoint-initdb.d/

EXPOSE 3306
