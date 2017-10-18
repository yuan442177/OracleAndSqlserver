# oracleתsqlserver��ѧ����֪ʶ��
## ʱ��ת��
#### ʱ���ʽ
```
oracle TO_DATE('{0} 00:00:00', 'YYYY-MM-DD HH24:MI:SS')  
sqlserver '{0} 00:00:00'

```
#### ʱ��ת�ı��ַ�
```
oracle to_char(UpLoadTime,'yyyy-MM-dd HH24:mi:ss')   
sqlserver Convert(varchar(100),UpLoadTime ,20)   
ʱ�亯��:sysdate  
ʱ�亯��:getdate()

```
#### �����ַ�
```
oracle ||  
sqlserver +
```



# ����

```
oracle xx(+)  (+)xx   
sqlserver left join right join

sqlserver: sp_rename 'TB_PASSWORD.identityto','identitys'; --->�������ֶ���
oracle: ��ѯ�ޱ����ݱ�����������from dual   
��:select 1 from dual;  

ȥ���ո�:  
oracle:trim(string)  
sqlserver:ltrim(rtrim(string))
```



## 20171018

```
��oracle����decode�������ڸ�����������ֵ--->1:decode(�ֶλ��ֶε����㣬ֵ1��ֵ2��ֵ3��  
--->2:decode(����,ֵ1,����ֵ1,ֵ2,����ֵ2,...ֵn,����ֵn,ȱʡֵ)

�ú����ĺ������£�  
IF ����=ֵ1 THEN  
��������RETURN(����ֵ1)  
ELSIF ����=ֵ2 THEN  
��������RETURN(����ֵ2)  
��������......  
ELSIF ����=ֵn THEN  
��������RETURN(����ֵn)  
ELSE  
��������RETURN(ȱʡֵ)  
END IF  

��sqlserver��û�����ƺ���ʹ��case when then end ��ģ��  
��: oracle-->decode(a.u_samplebatch,'',0,1)  
sqlserver-->case a.u_samplebatch when '' then 0 else 1 end

oracle:nvl(exp1,exp2)   ���exp1��Ϊ�գ�����exp1,���򷵻�exp2  
sqlserver:isnull(exp1,exp2)
```


### ��sqlserver��ʵ��oracle��lpad����

```
/*ʹ��ָ�����ַ����������ַ�����ָ������
**����ַ������ȴ���ָ�����ȣ������ַ�����ߵ��Ӵ�������Ϊָ������
*/
create function [dbo].[lpad](@s nvarchar(255),@length int,@char char(1))

returns nvarchar(255)

as

begin

declare @fullstring nvarchar(255) --������ַ���
declare @fillstring nvarchar(255) --�����ַ���
declare @filllen int --���ĳ���
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
