## 创建游标

## 创建函数

```sql
-- 最简单的仅有一条sql的函数
create function myselect2() returns int return 666;
select myselect2(); -- 调用函数

--
create function myselect3() returns int
begin 
    declare c int;
    select id from class where cname="python" into c;
    return c;
end;
select myselect3();
-- 带传参的函数
create function myselect5(name varchar(15)) returns int
begin 
    declare c int;
    select id from class where cname=name into c;
    return c;
end;
select myselect5("python");
```

### 提取数字或英文或中文

``` mysql 

DROP FUNCTION IF EXISTS Num_char_extract;
CREATE FUNCTION Num_char_extract (Varstring VARCHAR(100) CHARSET utf8, flag INT) RETURNS VARCHAR(50) CHARSET utf8
BEGIN
	DECLARE len INT DEFAULT 0;
	DECLARE Tmp VARCHAR(100) DEFAULT '';
	SET len=CHAR_LENGTH(Varstring);
	IF flag = 0 
	THEN
		WHILE len > 0 DO
		IF MID(Varstring,len,1)REGEXP'[0-9]' THEN
		SET Tmp=CONCAT(Tmp,MID(Varstring,len,1));
		END IF;
		SET len = len - 1;
		END WHILE;
	ELSEIF flag=1
	THEN
		WHILE len > 0 DO
		IF (MID(Varstring,len,1)REGEXP '[a-zA-Z]') 
		THEN
		SET Tmp=CONCAT(Tmp,MID(Varstring,len,1));
		END IF;
		SET len = len - 1;
		END WHILE;
	ELSEIF flag=2
	THEN
		WHILE len > 0 DO
		IF ( (MID(Varstring,len,1)REGEXP'[0-9]')
		OR (MID(Varstring,len,1)REGEXP '[a-zA-Z]') ) 
		THEN
		SET Tmp=CONCAT(Tmp,MID(Varstring,len,1));
		END IF;
		SET len = len - 1;
		END WHILE;
	ELSEIF flag=3
	THEN
		WHILE len > 0 DO
		IF NOT (MID(Varstring,len,1)REGEXP '^[u0391-uFFE5]')
		THEN
		SET Tmp=CONCAT(Tmp,MID(Varstring,len,1));
		END IF;
		SET len = len - 1;
		END WHILE;
	ELSE 
		SET Tmp = 'Error: The second paramter should be in (0,1,2,3)';
		RETURN Tmp;
	END IF;
	RETURN REVERSE(Tmp);
END;
```



### 去除前面后面连续指定的字符 和指定字符后的字符

``` mysql
CREATE FUNCTION rmbackzero(val VARCHAR(100),val_1 VARCHAR(100)) returns VARCHAR;  
begin 
DECLARE temp VARCHAR(100);  
DECLARE temp_1 VARCHAR(100);
DECLARE 1_temp VARCHAR(100);
DECLARE flag tinyint(1);
  if locate('-',val) <=> 0 then  -- 获取指定字符的位置
	set temp = val;
	else 
	set temp = left(val,locate('-',val)-1); 	-- 从左边开始截取
	end if; 
	
-- set temp_1 = mid(temp,LENGTH(temp));  -- 从多少位开始截取 -到多少位 截取最后一位
set temp_1 = right(temp,1); -- 从右边开始截取 截取最后一位
set 1_temp = left(temp,1);  -- 截取第一位
WHILE temp_1<=>val_1 DO
-- set temp = mid(temp,1,LENGTH(temp)-1);  -- 去掉最后最后一位
set temp = left(temp, length(temp)-1); -- 去掉右边最后一位
set temp_1 = right(temp,1);
END WHILE;

WHILE 1_temp<=>val_1 DO
set temp = right(temp, length(temp)-1); -- 去掉第一位 
set 1_temp = left(temp,1);
END WHILE;
-- 
-- if  temp REGEXP '[a-z]' then   -- 判断字符中是否存在英文
-- set temp = REPLACE(temp,'0',''); -- 替换字符中所有的 0
-- end if;
return temp;      
end
```

## 存储过程

```mysql
drop procedure if exists test;

CREATE PROCEDURE test(in val varchar(100))
BEGIN
	select val;
end;

CREATE PROCEDURE test()
BEGIN
	
	DECLARE n varchar(100);
	DECLARE c varchar(100);
	DECLARE n1 int default 1;
	declare done int default false;
	declare selects cursor for select dname,dvalue from emmp.emmpdict; -- 游标最后定义
	declare continue HANDLER for not found	set done = true;  
	
	open selects;
	
	repeat
	fetch selects into n,c;
			set n1 =n1+1;
	until done end repeat; 
	close selects;
	select n1;

end;

call test('运行');
call test();
```

### 自定义字典更据code生成层级

``` mysql
BEGIN
DECLARE  _isshow VARCHAR(10);
DECLARE  _id int;
DECLARE  _pid int;
DECLARE  _length int;
DECLARE  _dseq VARCHAR(100);
DECLARE  _pcode VARCHAR(100);
DECLARE  _code VARCHAR(100);
declare done int default false;
declare selects cursor for select id from emmp.emmpdict where dtype =_dict_type; -- 定义游标
declare continue HANDLER for not found	set done = true; -- 监控游标循环not found错误

set _isshow ='Y';
insert into emmp.emmpdict (dvalue,grade,dorder,dname,isshow,dtype) VALUES (_dict_type,1,0,_dict_typename,_isshow,_dict_type);   -- 插入字典头

insert into emmp.emmpdict (dvalue,grade,dorder,dname,isshow,dtype)  
select dict_id dvalue,length(pmsf.rmbackzero(dict_id,'0'))+1 grade,if(id is null,IF(Num_char_extract(pmsf.rmbackzero(dict_id,'0'),0)<=>'',0,Num_char_extract(pmsf.rmbackzero(dict_id,'0'),0)),id) dorder,
dict_name dname,_isshow,_dict_type from pmsf.sheet1 where dict_type = _dict_typename and dict_id is not null and dict_name is not null;   -- 插入基本数据

 open selects; -- 打开游标
 repeat  -- 循环 
 fetch selects into _id;  -- 赋值
 
      if not done then 
			
				select mid(pmsf.rmbackzero(dvalue,'0'),1, LENGTH(pmsf.rmbackzero(dvalue,'0')) -1 ) into _pcode from emmp.emmpdict where id = _id; -- 定义pcode pdvalue
-- 				select id into _pid from emmp.emmpdict where pmsf.rmbackzero(dvalue,'0') = _pcode  and dtype = _dict_type; 	-- 查询父id
			
				select max(length(pmsf.rmbackzero(dvalue,'0')))  into _length	 
				from emmp.emmpdict where dtype = _dict_type and locate(pmsf.rmbackzero(dvalue,'0'), _pcode);	
				
				select id  into _pid	from emmp.emmpdict where dtype = _dict_type and locate(pmsf.rmbackzero(dvalue,'0'), _pcode) 
				and length(pmsf.rmbackzero(dvalue,'0')) = _length;	
					
					if done then
					set done =false;
				  end if;
					
					if (_pid <=> null or _pid <=> _id ) then   -- 如果id为 设置字点头id
						select id into _pid from emmp.emmpdict where dtype =_dict_typename;
					end if;	
				
				update emmp.emmpdict set pid = _pid where id = _id ;
				
			  set _pid = null;
        	
			end if;	
 until done end repeat;  -- 结束循环
 
 close selects;					 -- 关闭游标

END
```

### 根据父级节点生成grade 

``` mysql
CREATE PROCEDURE `repeat_dict_grade`(in _dtype VARCHAR(100))
BEGIN
declare _id int;
declare __dtype VARCHAR(100);
declare __dvalue VARCHAR(100);
declare __grade int;
declare ___grade int;
declare _isgrade int default false;
declare done int default false;
declare selects cursor for select id from emmp.emmpdict where dtype like CONCAT('%',_dtype,'%') and dtype != dvalue; -- 定义游标
declare continue HANDLER for not found	set done = true; -- 监控游标循环not found错误

 open selects; -- 打开游标
 repeat  -- 循环 
 fetch selects into _id;  -- 赋值
 
		select dtype,dvalue,grade into __dtype,__dvalue,__grade from emmp.emmpdict where id =_id ;
		select (count(0)+1) into ___grade from emmp.emmpdict where locate(pmsf.rmbackzero(dvalue,'0'),pmsf.rmbackzero(__dvalue,'0'))
		and dtype=__dtype ;
		set _isgrade = (__grade != ___grade);
		
		if _isgrade then 
		update emmp.emmpdict set grade = ___grade where id = _id;
	  end if; 
	
 until done end repeat;  -- 结束循环
 
 close selects;					 -- 关闭游标

END
```

## 其他样例
### 表注释批量处理

``` mysql 
SELECT     
concat(    
    'alter table ',     
    table_schema, '.', table_name,     
    ' modify column ', column_name, ' ', column_type, ' ',     
    if(is_nullable = 'YES', ' ', 'not null '),     
    if(column_default IS NULL, '',     
        if(    
            data_type IN ('char', 'varchar')     
            OR     
            data_type IN ('date', 'datetime', 'timestamp') AND column_default != 'CURRENT_TIMESTAMP',     
            concat(' default ''', column_default,''''),     
            concat(' default ', column_default)    
        )    
    ),     
    if(extra is null or extra='','',concat(' ',extra)),  
    ' comment ''', b.zdzs, ''';'    
) s    
FROM information_schema.columns a ,(select distinct zdm,zdzs from tablecomment) b   
WHERE table_schema = 'emmp'  and  b.zdm =a.column_name and a.column_comment ='' and b.zdzs !='';
```



