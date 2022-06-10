# ORACLE笔记

## 修改数据库表字段类型

假设有一表tb，字段名为name，类型为oldType，修改后类型为newType

### 1.对应字段无数据

直接修改

```sql
alter table tb modify column(name newType);
```

### 2.对应字段有数据，修改后类型兼容旧类型

例如oldType=nchar(20)，newType=nvarchar2(20)，可以直接修改

```sql
alter table tb modify (name nvarchar2(20));
```

### 3.对应字段有数据，修改后类型不兼容旧类型

例如oldType=nchar(20)，newType=varchar2(40)，直接修改会报错"ORA-01439:要更改数据类型,则要修改的列必须为空"，需要按以下顺序操作：

- 如果不考虑字段顺序（字段顺序改变可能对sqlldr有影响）
  
#### 1.修改原字段名为name_tmp

```sql
alter table tb rename column name to name_tmp;
```

#### 2.增加原字段名，类型为新类型

```sql
alter table tb add column name varchar2(40);
```

#### 3.将原类型字段名数据赋值到新类型字段

这里应当注意使用函数对原类型字段处理以适配新类型字段

```sql
update tb set name=trim(name_tmp);
```

#### 4.删除旧类型字段

```sql
alter table tb drop column name_tmp;
```

- 若要保持原字段顺序

1. 增加tmp字段
2. 复制数据到tmp字段，原字段值置空
3. 修改字段类型
4. 将数据复制回来
5. 删除tmp字段

## 数据统计：按日、周、月、季度、年

这里所说统计是指数据表table中date字段和当前系统时间sysdate的时间差

### 每日

### 每周

### 每月

```sql
select sysdate,t.date,ceil(months_between(sysdate,t.date)) dif 
from table t
where add_months(t.date,ceil(months_between(sysdate,t.date)))<=sysdate;
```

### 每季度

```sql
select sysdate,t.date,ceil(months_between(sysdate,t.date)) dif 
from table t
where add_months(t.date,ceil(months_between(sysdate,t.date)/3)*3)<=sysdate;
```

### 每年

```sql
select sysdate,t.date,ceil(months_between(sysdate,t.date)) dif 
from table t
where add_months(t.date,ceil(months_between(sysdate,t.date)/12)*12)<=sysdate;
```

## 数据导出导入与数据泵导出导入

### 前提条件

使用expdb命令导出和使用impdb命令导入时，转储文件只能存放在DIRECTORY对象对应的系统目录，必须先创建DIRECTORY对象，并为数据库用户赋予权限

#### 1.查询DIRECTORY对象

```sql
select * from dba_directories;
```

### 2.新建DIRECTORY对象

```sql
CREATE OR REPLACE DIRECTORY dir_exp AS '/home/oracle/dump/exp';
```

#### 3.赋权

```sql
GRANT read,write ON DIRECTORY dir_exp TO test;
```

### 导出

1.

### 导入

### 区别
