## 流程

1. 以MySQL数据库为例，创建api数据库，并创建表student，插入两条数据：

mysql> select * from student;

+----+-------+

| id | name  |

+----+-------+

|  0 | hqq   |

|  1 | hzwww |

+----+-------+

2 rows in set (0.01 sec)


2. 根据数据库创建beego api．使用命令：

fm@hzw　~/go/src/github.com/BigoSprite $ bee api beegoApiAppExample -conn=root:root@tcp\(127.0.0.1\)/api

其中，api为MySQL数据库, root:root分别为数据库的用户名和密码


3. 切换到beegoApiAppExample目录，生成api文档．使用命令：

fm@hzw　~/go/src/github.com/BigoSprite $ bee run -gendoc=true -downdoc=true

在浏览器中输入：http://localhost:8080/swagger，即可查看文档．

4. 创建home.html［见beegoApiAppExample/htdocs/home.html］，使用axios作为http请求库．使用浏览器打开，F12查看network中的请求详情页．可得到GET请求返回的数据．
