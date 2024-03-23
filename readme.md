# Thanos: DBMS Bug Detection via Storage Engine Rotation Based Differential Testing

The artifact consists of the following contents:

An implementation of Thanos to do DBMS Testing for target DBMSs in the `Tool` directory.

A tutorial to introduce how to use Thanos in readme.md.

A bug list to introduce the anomalies detected by Thanos in bug.md.

The storage engine features used by Thanos in the `StorageEngineFeature` directory.



# Environment for Thanos

1. OS:
   Ubuntu20.04

2. Install the following C libraries:
    fmt
    odbc
    boost_regex
    boost_serialization
    boost_program_options
    thrift
    pqxx
    pthread

3. Download the ODBC driver from the website and write the correct path in the odbc.ini

```sh
Drive="****/libmyodbc8a.so"
```

# Perform Testing

## MySQL

Pull the docker image from the website:

```sh
docker pull mysql:8.0.32
```

Create several docker containers from the image:

```sh
docker run --name mysql8a -p 3388:3306 -e MYSQL_ROOT_PASSWORD=123456  -d mysql:8.0.32
docker run --name mysql8b -p 3388:3400 -e MYSQL_ROOT_PASSWORD=123456  -d mysql:8.0.32
...
```

Create an empty database in MySQL.

```sh
docker exec -it mysql8a bash
mysql -uroot -p123456
create database test;
...
```

Run Testing With Thanos

```sh
./Thanos engine project_mysql8 mysql8a mysql8b
```

The result of DBMS testing would be saved in dir ''project_mysql8''.

## MairaDB

Pull the docker image from the website:

```sh
docker pull mariadb:10
```

Create several docker containers from the image:

```sh
sudo docker run --name mariadb10a -p 3488:3306 -e MYSQL_ROOT_PASSWORD=123456  -d mariadb:10
sudo docker run --name mariadb10b -p 3500:3306 -e MYSQL_ROOT_PASSWORD=123456  -d mariadb:10
...
```

Create an empty database in MariaDB.

```sh
docker exec -it mariadb10a bash
mysql -uroot -p123456
create database test;
...
```

Run Testing With Thanos

```sh
./Thanos engine project_mariadb10 maraidb10a maraidb10b
```

The result of DBMS testing would be saved in dir ''project_mariadb10''.

## Percona

Pull the docker image from the website:

```sh
docker pull percona:8.0
```

Create several docker containers from the image:

```sh
sudo docker run --name percona8a -p 3588:3306 -e MYSQL_ROOT_PASSWORD=123456  -d percona:8.0
sudo docker run --name percona8b -p 3600:3306 -e MYSQL_ROOT_PASSWORD=123456  -d percona:8.0
...
```

Create an empty database in Percona.

```sh
docker exec -it percona8a bash
mysql -uroot -p123456
create database test;
...
```

Run Testing With Thanos

```sh
./Thanos engine project_percona8 percona8a percona8b 
```

The result of DBMS testing would be saved in dir ''project_percona8''.
