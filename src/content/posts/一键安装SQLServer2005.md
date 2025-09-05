---
title: 一键安装SQLServer2005
pubDate: 2025-09-05
categories: ['折腾']
description: ''
---

```
@echo off
set curdir=%~dp0
set SystemDrive_xn=c:
set WINSYSDIR_xn=%windir%\system32
cd /d %curdir%

echo 正在安装 msiexec服务 ......................
msiexec /regserver /quiet
sc.exe config msiserver start= auto


if /i "%PROCESSOR_IDENTIFIER:~0,3%" == "x86" goto X64

echo 正在安装 MICROSOFT SQL SERVER 2005 EXPRESS EDITION SERVICE PACK 4 X64 ......................
start /wait cn_sql_server_2005_express_edition_service_pack_4_x64.exe /qb INSTANCENAME=MSSQLSERVER ADDLOCAL=SQL_Engine SECURITYMODE=SQL SAPWD=sa INSTALLSQLDATADIR="C:\\Program Files\\Microsoft SQL Server\\" SQLAUTOSTART=1 DISABLENETWORKPROTOCOLS=2
echo 正在安装 Microsoft SQL Server Management Studio Express X64......................
msiexec /i SQLServer2005_SSMSEE_x64.msi /quiet /passive
exit

:X86
echo 正在安装 MICROSOFT SQL SERVER 2005 EXPRESS EDITION SERVICE PACK 4 X86 ......................
start /wait cn_sql_server_2005_express_edition_service_pack_4_x86.exe /qb INSTANCENAME=MSSQLSERVER ADDLOCAL=SQL_Engine SECURITYMODE=SQL SAPWD=sa INSTALLSQLDATADIR="C:\\Program Files\\Microsoft SQL Server\\" SQLAUTOSTART=1 DISABLENETWORKPROTOCOLS=2
echo 正在安装 Microsoft SQL Server Management Studio Express X86 ......................
msiexec /i SQLServer2005_SSMSEE.msi /quiet /passive
```