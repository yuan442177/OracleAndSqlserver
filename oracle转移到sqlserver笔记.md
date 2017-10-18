# oracle转sqlserver中学到的知识点
## 时间转换
#### 时间格式
```
oracle TO_DATE('{0} 00:00:00', 'YYYY-MM-DD HH24:MI:SS')  
sqlserver '{0} 00:00:00'

```
#### 时间转文本字符
```
oracle to_char(UpLoadTime,'yyyy-MM-dd HH24:mi:ss')   
sqlserver Convert(varchar(100),UpLoadTime ,20)   
时间函数:sysdate  
时间函数:getdate()

```
#### 链接字符
```
oracle ||  
sqlserver +
```



# 所有

```
oracle xx(+)  (+)xx   
sqlserver left join right join

sqlserver: sp_rename 'TB_PASSWORD.identityto','identitys'; --->重命名字段名
oracle: 查询无表数据必须加上虚拟表from dual   
如:select 1 from dual;  

去除空格:  
oracle:trim(string)  
sqlserver:ltrim(rtrim(string))
```



## 20171018

```
在oracle中有decode函数用于根据条件返回值--->1:decode(字段或字段的运算，值1，值2，值3）  
--->2:decode(条件,值1,返回值1,值2,返回值2,...值n,返回值n,缺省值)

该函数的含义如下：  
IF 条件=值1 THEN  
　　　　RETURN(翻译值1)  
ELSIF 条件=值2 THEN  
　　　　RETURN(翻译值2)  
　　　　......  
ELSIF 条件=值n THEN  
　　　　RETURN(翻译值n)  
ELSE  
　　　　RETURN(缺省值)  
END IF  

在sqlserver中没有类似函数使用case when then end 来模仿  
如: oracle-->decode(a.u_samplebatch,'',0,1)  
sqlserver-->case a.u_samplebatch when '' then 0 else 1 end

oracle:nvl(exp1,exp2)   如果exp1不为空，返回exp1,否则返回exp2  
sqlserver:isnull(exp1,exp2)
```


### 在sqlserver中实现oracle的lpad函数

```
/*使用指定的字符从左边填充字符串至指定长度
**如果字符串长度大于指定长度，返回字符串左边的子串，长度为指定长度
*/
create function [dbo].[lpad](@s nvarchar(255),@length int,@char char(1))

returns nvarchar(255)

as

begin

declare @fullstring nvarchar(255) --填充后的字符串
declare @fillstring nvarchar(255) --填充的字符串
declare @filllen int --填充的长度
declare @i int

if @length<=len(@s)
return left(@s,@length)

set @filllen=@length-len(@s)
set @i=0


while(@i<@filllen)
begin
set @fillstring=isnull(@fillstring,'')+@char
set @i=@i+1
end

set @fullstring=@fillstring+@s
return @fullstring

end

GO
```
