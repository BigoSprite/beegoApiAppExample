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


3. 切换到beegoApiAppExample目录，生成swagger文档．使用命令：

        fm@hzw　~/go/src/github.com/BigoSprite $ bee run -gendoc=true -downdoc=true

    在浏览器中输入：http://localhost:8080/swagger，即可查看文档．

4. 创建home.html［见beegoApiAppExample/htdocs/home.html］，使用axios作为http请求库．使用浏览器打开，F12查看network中的请求详情页．可得到GET请求返回的数据．

5. 数据库增加新的表

    5.1 使用如下命令添加新的model和controller：

	    $ bee api beegoApiAppExample -tables="addedTableName" -conn=root:root@tcp\(127.0.0.1:3306\)/api
	［   注意］不要更新［routers］文件，不然之前的路由全部没了，需要手动添加新表的路由！切记！

    5.2 切换到工程目录下，使用如下命令生成新的swagger文档：

	    $ bee run -gendoc=true -downdoc=true 
    执行完毕，即可查看新的swagger文档

## AJAX跨域请求

在main.go中添加如下代码：


	// ...
   	//　CORS 跨域请求 参考:https://gocn.io/question/426
	beego.InsertFilter("*", beego.BeforeRouter, cors.Allow(&cors.Options{
		AllowAllOrigins:  true,
		AllowMethods:     []string{"GET", "POST", "PUT", "DELETE", "OPTIONS"},
		AllowHeaders:     []string{"Origin", "Authorization", "Access-Control-Allow-Origin", "Access-Control-Allow-Headers", "Content-Type"},
		ExposeHeaders:    []string{"Content-Length", "Access-Control-Allow-Origin", "Access-Control-Allow-Headers", "Content-Type"},
		AllowCredentials: true,
	}))
	//　beego.Run()










