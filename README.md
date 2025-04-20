# Convert Epoch to Datetime2 for SQL Server 2008+
SQL Server: Convert Epoch to Datetime2

#Usage

DECLARE @SQLTimezone varchar(2048) --the TZ  
declare @epochms varchar(50)  

--time zone name as given by the query: select * from sys.time_zone_info order by name  
set @SQLTimezone = 'Central European Standard Time'  
set @epochms = '1745098816793' --2025-04-19 23:40:16.793  

--input is epoch in milliseconds as string, UTC  
select dbo.fnConvertEpochToDatetime2(@epochms, @SQLTimeZone)  

#Source Code  

create or function dbo.fnConvertEpochToDatetime2(@epochms varchar(50), @SQLTimezone varchar(2048) = 'UTC' )  
returns datetime2(3)  
as  
begin  
&nbsp;--NOTE! input @epochms is assumed to be given in milliseconds since 1970-01-01  
&nbsp;declare @epoch int  
&nbsp;declare @ms int  
&nbsp;declare @utcdate datetime2(3)  
&nbsp;declare @epochdayone datetime2(3)  
&nbsp;set @epochdayone = '1970-01-01 00:00:00.000'  
&nbsp;set @ms = convert(int, right(@epochms,3))  
&nbsp;set @epoch = convert(int, left(@epochms, len(@epochms)-3))  
&nbsp;set @utcdate = dateadd(millisecond, @ms, dateadd(s, @epoch, @epochdayone))  
&nbsp;return format(@utcdate at time zone 'UTC' at time zone @SQLTimezone,'yyyy-MM-dd HH:mm:ss.fff')  
end  
