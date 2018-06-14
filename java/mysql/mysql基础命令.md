#mysql命令：
##启动
```
net start mysql
```

##进入mysql环境（登录）
```mysql -hlocalhost -uroot -p```

##查看数据库
```show databases;```

##查看用户表
```SELECT * FROM mysql.user```

##查看用户权限
```SELECT User,Host,Grant_priv FROM mysql.user where user='root';```

##创建用户
```
 insert into mysql.user(Host,User,Password) values("localhost","test",password("1234"));
```

##对用户授权
```
// all privileges  表示所有权限
// *.*   databases:tables
// 'senninha'@'localhost' 用户@端口 
// identified by ''  password
grant all privileges on *.* to 'senninha'@'localhost' identified by '' with grant option;
```

