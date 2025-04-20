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

Two versions 

1. dbo.fnConvertEpochToDatetime2
   Takes the epoch timestamp as a string

2. dbo.fnConvertBigIntEpochToDatetime2
   Takes the epoch timestamp as a bigint
