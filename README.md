
# Project Sister



## Replikasi Server

### Server 1

Setting ufw for mysql

```bash
  sudo ufw allow from any to any port 3306 proto tcp  
```

Change configure mysqld.cnf

```bash
  sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
Restart mysql

```bash
  sudo service mysql restart
```
Setting database mysql master

```bash
  mysql -uroot
  create user 'repl'@'ipSlave' identified by 'password';
  grant replication slave on *.* to 'repl'@'ipSlave';
  show master status \G
```

### Server 2

Setting ufw for mysql

```bash
  sudo ufw allow from any to any port 3306 proto tcp  
```

Change configure mysqld.cnf

```bash
  sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
Restart mysql

```bash
  sudo service mysql restart
```
Setting database mysql slave

```bash
  mysql -uroot
  change replication source to source_host='ipMaster', source_log_file='FileNameMaster', source_log_pos=PositionMaster, source_ssl=1;
  start replica user='repl' password='Password';
  show replica status \G
```