# MySQl

Javaweb

## 一、基础篇

### 1、概述

![image-20231106075617194](https://gitee.com/coi4/test/raw/master/img/image-20231106075617194.png)

 关系型数据库（RDBMS）：建立在关系模型基础上，由多张相互连接的二维表组成的数据库（基于**二维表**存储数据的数据库就成为关系型数据库，不是基于二维表存储数据的数据库，就是非关系型数据库）；所谓二维表，指的是**由行和列组成的表**

特点：

1. 使用表存储数据，格式统一，便于维护。
2. 使用SQL语言操作，标准统一，使用方便。

可以通过MySQL客户端连接数据库管理系统DBMS，然后通过DBMS操作数据库。

可以使用SQL语句，通过数据库管理系统操作数据库，以及操作数据库中的表结构及数据。

一个数据库服务器中可以创建多个数据库，一个数据库中也可以包含多张表，而一张表中又可以包含多行记录

### 2、SQL

SQL语言，是操作关系型数据库的 **统一标准**

语法、分类：见javaweb；DDL定义，DML操作，DQL查询，DCL控制；

**DCL**：DCL英文全称是**Data Control Language**(数据控制语言)，用来管理数据库用户、控制数据库的访问权限。

**管理用户**：

- 查询用户：select * from mysql.user; 

  -  Host代表当前用户访问的主机, 如果为localhost, 仅代表只能够在当前本机访问，是不可以远程访问的。 User代表的是访问该数据库的用户名。在MySQL中需要通过Host和User来唯一标识一个用户

-  创建用户：CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';

  ```
  创建用户heima, 可以在任意主机访问该数据库, 密码123456;
  create user 'heima'@'%' identified by '123456';
  ```

  ```
  创建用户itcast, 只能够在当前主机localhost访问, 密码123456;
  create user 'itcast'@'localhost' identified by '123456';
  ```

- 修改用户密码：ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码' ; 

-  删除用户：DROP USER '用户名'@'主机名' ; 

在MySQL中需要通过用户名@主机名的方式，来唯一标识一个用户。

主机名可以使用 % 通配。

这类SQL开发人员操作的比较少，主要是DBA（ Database Administrator 数据库管理员）使用。

**权限控制**：**官方文档**

- 查询权限:SHOW GRANTS FOR '用户名'@'主机名' ; 
- 授予权限:GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名'; 
- 撤销权限:REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名'; 

**多个权限之间，使用逗号分隔**

 授权时， 数据库名和表名可以使用 * 进行通配，代表所有。

### 3、函数

函数 是指一段可以直接被另一段程序调用的程序或代码

MySQL中的函数主要分为以下四类： 字符串函数、数值函数、日期函数、流程函数。

**字符串函数**:![image-20231106091123941](https://gitee.com/coi4/test/raw/master/img/image-20231106091123941.png)

```
由于业务需求变更，企业员工的工号，统一为5位数，目前不足5位数的全部在前面补0。比如： 1号员
工的工号应该为00001。
update emp set workno = lpad(workno, 5, '0');
```

**数值函数**:

![image-20231106091345775](https://gitee.com/coi4/test/raw/master/img/image-20231106091345775.png)

```
通过数据库的函数，生成一个六位数的随机验证码。
select lpad(round(rand()*1000000 , 0), 6, '0');
```

**日期函数**:

![image-20231106091516902](https://gitee.com/coi4/test/raw/master/img/image-20231106091516902.png)

```
查询所有员工的入职天数，并根据入职天数倒序排序。
select name, datediff(curdate(), entrydate) as 'entrydays' from emp order by
entrydays desc;
```

**流程函数**:

![image-20231106091604398](https://gitee.com/coi4/test/raw/master/img/image-20231106091604398.png)

```
select
id,
name,
(case when math >= 85 then '优秀' when math >=60 then '及格' else '不及格' end )
'数学',
(case when english >= 85 then '优秀' when english >=60 then '及格' else '不及格'
end ) '英语',
(case when chinese >= 85 then '优秀' when chinese >=60 then '及格' else '不及格'
end ) '语文'
from score;
```

### 4、约束

概念：约束是作用于表中字段上的规则，用于限制存储在表中的数据。3.1.2.2

图形化界面来创建表结构时，如何来指定约束:![image-20231106092143210](https://gitee.com/coi4/test/raw/master/img/image-20231106092143210.png)

删除外键:

```
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

删除更新行为:添加了外键之后，再删除父表数据时产生的约束行为，我们就称为删除/更新行为![image-20231106092708918](https://gitee.com/coi4/test/raw/master/img/image-20231106092708918.png)

语法:

```
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段) REFERENCES
主表名 (主表字段名) ON UPDATE CASCADE ON DELETE CASCADE;
```

CASCADE：

```
alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references
dept(id) on update cascade on delete cascade ;
//修改父表id为1的记录，将id修改为6，在子表中dept_id值为1的记录，现在也变为6了---级联
```

在一般的业务系统中，不会修改一张表的主键值。

SET NULL：

```
alter table emp add constraint fk_emp_dept_id foreign key (dept_id) references
dept(id) on update set null on delete set null ;
//删除外键 fk_emp_dept_id。然后再通过数据脚本，将emp、dept表的数据恢复。删除id为1的数据，父表的数据删除之后，打开子表 emp，发现子表emp的dept_id字段，原来dept_id为1的数据，现在都被置为NULL了
```

### 5、多表查询

3.1.3

### 6、事务

3.2.4

## 二、运维篇

### 1、日志

### 2、主从复制

### 3、分库分表

### 4、读写分离

## 三、进阶篇

### 1、存储引擎

### 2、索引

### 3、SQL优化

### 4、视图/存储过程/触发器

### 5、锁

### 6、InnoDB引擎

### 7、MySQl管理

## 总结

下载安装mysql；下载安装DataGrip，或使用**idea**（替换命令行操作）

命令行连接mysql、sql注释

- 库：查询、切换、创建、删除
- 表：创建（约束、数据类型、时间）、查询（+多表查询）、修改、删除
- 数据：添加、修改、删除、查询

多表设计操做+案例

手动提交事务控制

索引：创建、查询数据（使用索引）、查看、删除

```
public class sy_p3 {
  public static void main(String[] args) throws Exception {
    Scanner sc=new Scanner(System.in);
    system s=new system();
    while (true){
      System.out.println("请输入服务序列号：");
      System.out.println("1.添加学生信息");
      System.out.println("2.查看成绩排序结果");
      System.out.println("输入'999'退出系统");
      int a=sc.nextInt();
      sc.nextLine();
      if(a==1){
        System.out.println("请分别输入学生学号、姓名、英语成绩、数学成绩（回车两次录入结束）：");
        while (true) {
          String input = sc.nextLine();
          if (input.trim().isEmpty()) {
            break;
          }
          String[] parts = input.split("\\s+");
          int num = Integer.parseInt(parts[0]);
          String name = parts[1];
          int English = Integer.parseInt(parts[2]);
          int Math = Integer.parseInt(parts[3]);
          s.insertData(num,name,English,Math);
          s.count++;
        }
          }else if(a==2){
        System.out.println("排序后的顺序为：");
        s.sort();
      }else if(a==999){
        break;
      }
    }
  }


}
class system{
  SeqList L=new SeqList(10000);
  int count=0;
  public void insertData(int num,String name,int Englis,int Math) throws Exception {
    student stu=new student(num,name,Englis,Math);
    L.insert(count,new RecordNode(stu.totalScore,stu));
  }
  public void sort(){
    RecordNode temp;
    int i, j;
    for (i = 1; i <count; i++) {
      temp = L.r[i];
      for (j = i - 1; j >= 0 && temp.key.compareTo(L.r[j].key) > 0; j--) {
        L.r[j + 1] = L.r[j];
      }
      L.r[j + 1] = temp;
    }
    for (int k = 0; k < count; k++) {
      System.out.println(L.r[k].element);
    }
  }
}
class student{
  public int num;
  public String name;
  public int EnglisScore;
  public int MathScore;
  public int totalScore;

  public student(int num, String name, int englisScore, int mathScore) {
    this.num = num;
    this.name = name;
    EnglisScore = englisScore;
    MathScore = mathScore;
    totalScore=EnglisScore+MathScore;
  }

  @Override
  public String toString() {
    return "学号："+num+" "+"姓名："+name+" "+"英语："+EnglisScore+" "+"数学："+MathScore+" "+"总分："+totalScore;
  }
}
```

## 实验七 排序的操作试验

> **实验日期**：2024.04.23      **实验地点**：科技楼4074      **仪器编号**：029   **学号**：170106   **姓名**：TOM   

### 一、实验目的

> (1)熟悉并掌握几种排序方法的基本思想及实现。 (2)掌握排序算法性能优劣比较的实现技术。 (3)了解排序的实际功能。

------

------

### 二、实验内容

**1-2实验随机序列，统一使用种子2024**

> (1)编写程序,要求使用带监视哨的直接插人排序算法对20个0~ 100之间的随机整数进行排序(验证性内容)。 (2)编写程序,比较冒泡排序与快速排序两种排序算法的优劣(设计性内容)。 (3)编写程序，对学生成绩表计算总分并按总分从小到大排序并输出(应用设计性内容)。

------

------

> 在Java中，要产生相同的随机数序列，你可以使用一个固定的种子来初始化Random类的实例。这会使得使用相同的种子值的不同Random实例产生相同的随机数序列。 下面是一个示例代码，演示如何使用固定种子值来产生相同的随机数序列：

```
import java.util.Random; public class ReproducibleRandomSequence {    public static void main(String[] args) {        // 使用固定的种子值        long seed = 12345L;         Random random1 = new Random(seed);        Random random2 = new Random(seed);         // 生成相同的随机数序列        for (int i = 0; i < 5; i++) {            System.out.println(random1.nextInt()); // 使用random1生成并打印随机数            System.out.println(random2.nextInt()); // 使用random2生成并打印相同的随机数        }    }}
```

在这个例子中，random1和random2都使用了相同的种子值12345L，因此它们生成的随机数序列是完全相同的。每次运行此代码，它都会打印出两个序列相同的随机数对。 提示：AI自动生成，仅供参考

------

------

### 三、实验结果

> 1.验证性内容。      **此处为实验截图**

------

------

> 2.设计性内容。      **此处为实验截图**

------

------

> 3.应用设计性内容。      **此处为实验截图**

------

------

### 四、实验总结

  遇到的问题及解决方法 && 相关知识点的学习心得和经验总结