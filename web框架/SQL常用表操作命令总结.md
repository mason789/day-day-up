+ 建表

	create table <表名> (<字段> <类型>，。。。)
	create table user(id int(4) not null primary key auto_increment,
						name char(20) not null, sex int(4));
						
+ 获取表结构

	desc <表名>
	desc user;
	
+ 删除表

	drop table <表名>
	drop table user;
	
+ 插入数据

	insert into <表名> (<字段1>，<字段2>。。) values(<值1>，<值2>。。。);  按需插入
	insert into <表名> values(<值。。>))   全部字段插入
	
+ 修改数据
	
	update <表名> set <字段>=<值> where <字段>=<值>
	
+ 查询数据

	select <字段> from <表名> where <字段>=<值>
	
+ 删除数据

	delete from <表名> where <字段>=<值>
	
+ 升序降序

	asc（升序默认）  desc(降序)
	