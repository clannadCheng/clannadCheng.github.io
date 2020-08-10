# oracle 基础知识

## 系统表操作

1、查询表注释

```
SELECT * FROM USER_TAB_COMMENTS;

三列：TABLE_NAME,TABLE_TYPE,COMMENTS
```

2、查询字段注释

```
SELECT * FROM USER_COL_COMMENTS;

三列：TABLE_NAME,COLUMN_NAME,COMMENTS
```

3、添加表注释

```
COMMENT ON TABLE STUDENT_INFO IS '表注释';

语法：COMMENT ON TABLE 表名 IS '表注释';
```

4、添加字段注释

```
COMMENT ON COLUMN STUDENT_INFO.STU_ID IS '列注释';

语法：COMMENT ON COLUMN 表名.字段名 IS '字段注释';
```

5、查看当前登录的用户的表:

```sql
 select table_name from user_tables;
```





## 回滚回退

`rollback;`
# oracle 函数

```
CREATE OR REPLACE FUNCTION FunctionName (
    --传入参数
    para NCHAR
) RETURN NUMBER IS
    --函数内使用的临时变量
    b1   NUMBER(38,0);
    n      NUMBER(38,0);
BEGIN
    --函数体
    。。。
   	return b1;
END;    
```



# oralce 代码块
## BEGIN END
```
begin  
Proc_Test(); --调用存储过程 or exec 
end; 
```
## DECLARE BEGIN END 游标
```sql
DECLARE
  testsql varchar(500); -- 声明变量
begin
  testsql:='update REGIST_OBJ_T set update_date = to_date('''||sysdate||''',''YYYY-MM-DD'') where reg_id =1'; -- 赋值
  Dbms_Output.put_line(testsql); 
  --打印 若不显示、执行开启打印sql set serveroutput on; 
  execute immediate testsql; --执行字符sql
  -- execute immediate 'select count(1) from emp' into l_cnt; --sql赋值
  -- execute immediate 'select dname, loc from dept where deptno = :1'   
  -- into l_nam, l_loc   
  -- using l_dept ;  --传递并检索值.INTO子句用在USING子句前
  
  EXCEPTION  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE ('Exception happened,data was rollback');
end;
```
### 游标类型

``` sql
    declare  
     stu_cur sys_refcursor;  
     stuone students%rowtype;  --指定表的类型
          begin  
       --这句赋值方式for   
       open stu_cur for select * from students;  
       --fetch赋值给rowtype   
       fetch stu_cur into stuone;  
            loop  
         dbms_output.put_line(stuone.name||' '||stuone.hobby);  
         fetch stu_cur into stuone;   --输出
         exit when stu_cur%notfound;  --未发现退出
       end loop;  
     end;  

--另一个游标使用方式 发现了在循环
declare  
     
   stu_cur sys_refcursor;   --做为参数传递结果集; 
   stuone students%rowtype;   
     
   begin  
     open stu_cur for select * from students;  
     fetch stu_cur into stuone;   
     --特别注意循环条件的改变   
     --这个条件是发现了在循环   
     --与上一个notfound不同的   
     while stu_cur%found loop   
       dbms_output.put_line(stuone.name||' '||stuone.hobby);  
       fetch stu_cur into stuone;  --输出 关闭游标？
     end loop;  
   end; 
   
--自定义rowtype;
declare   
   type empdtlrec is record (empno   number(4),   
                            ename   varchar2(20),   
                            deptno   number(2));   
   empdtl empdtlrec;   
begin   
   execute immediate 'select empno, ename, deptno ' ||   
                    'from emp where empno = 7934'   
     into empdtl;   
end; 
```



## 存储过程
```
create or replace procedure gb_error_updatetime
--定义输入输出  (num_A in integer,num_B out integer) 
as
 cursor cur is select cd_id,table_name from gbsj_error;
 updates_sql varchar2(500);
begin

  for temp in cur loop
  
    if temp.table_name='tsjb_complaint_info' 
    then  
    updates_sql:='update REGIST_OBJ_T set update_date = to_date('''||to_char(sysdate,'YYYY-MM-DD')||''',''YYYY-MM-DD'') where reg_id ='||temp.cd_id;     
     
    elsif temp.table_name='tsjb_complaint_info' --注意写法elsif
    then 
    updates_sql:='update REGIST_PROVIDER_T set update_date = to_date('''||to_char(sysdate,'YYYY-MM-DD')||''',''YYYY-MM-DD'') where reg_id ='||temp.cd_id;
     
    end if; --结束判断
    
    Dbms_Output.put_line(updates_sql);
    execute immediate updates_sql;
    
  end loop;
 
  commit;

end gb_error_updatetime;
```



# oracle 高级查询样例

## 正则

```sql
select regexp_replace('exe_research_ask_notes？(询问笔录)',
 '[^'|| unistr('\0391') || '-' || unistr('\9fa5') || ']','') from dual;  
 --提取中文
select regexp_replace('exe_researchaA_ask_notes？(询问笔录)', 
'[^a-zA-Z_]') from dual;
-- 提取指定符号和a-Z 
```

## 检查是否启动
`ps -ef | grep ora`

## 管理员登录
`sqlplus / as sysdba`
### 切换
`conn / as sysdba`
## 启动  
`startup`

## 启动数据库到挂载模式
`startup mount`  

## 停止服务
`shutdown immediate` 
## 强转停止
`shutdown abort`

> exit sql
## 启动和停止监听器 
```
lsnrctl start
lsnrctl stop
```

[^'|| unistr('\0391') || '-' || unistr('\9fa5') || ']: 