---
title: AuditLogs
author: rxcontributorone
category: rxwebcore
---

# AuditRequest

Auditing a server request keeps a track and log of details while any HTTP request is made. It contains information about which user has made request on which application module including its path, method name, timezone and created date.   

> If any unauthenticated user makes request than the user information is not stored.

The following data is stored in AuditRequest 

<table>
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>AuditRequestId</td><td>Id of Audit Request(PK)</td><td>int</td></tr>
<tr><td>UserId</td><td>Id of User(Based upon UserClaim)</td><td>int</td></tr>
<tr><td>ApplicationModuleId</td><td>Id of application module</td><td>int</td></tr>
<tr><td>MainRecordId</td><td>Id of the record</td><td>varchar(100)</td></tr>
<tr><td>Uri</td><td>Http request path</td><td>varchar(1024)</td></tr>
<tr><td>RequestMethod</td><td>request method name</td><td>varchar(10)</td></tr>
<tr><td>CreatedDate</td><td>request creation date</td><td>datetime</td></tr>
</table>

# AuditRecord

AuditRecord keeps a track and log of information whenever any data operation is done on any of the entity.

The following data is stored in AuditRecord

<table>
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>AuditRecordId</td><td>Id of Audit Record(PK)</td><td>int</td></tr>
<tr><td>AuditRequestId</td><td>Id of Audit Request(FK AuditRequest)</td><td>int</td></tr>
<tr><td>EventTypes</td><td>type of operation done</td><td>varchar(9)</td></tr>
<tr><td>TableName</td><td>Name of Table</td><td>varchar(50)</td></tr>
<tr><td>RecordId</td><td>Id of new entity added</td><td>varchar(100)</td></tr>
<tr><td>RecordName</td><td>Name of new entity added</td><td>nvarchar(MAX)</td></tr>
</table>

# AuditRecordDetails

Whenever entity is modified AuditRecordDetails keeps a track and log of information of oldValue, newValue, ColumnName and reference table where the updation is done.

The following data is stored in AuditRecordDetails

<table>
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>AuditRecordDetailId</td><td>Id of Audit Record Detail(PK)</td><td>int</td></tr>
<tr><td>AuditRecordId</td><td>Id of Audit Record(FK AuditRecord)</td><td>int</td></tr>
<tr><td>ColumnName</td><td>Name of column where data is modified</td><td>varchar(50)</td></tr>
<tr><td>OldValue</td><td>Old Entity object value</td><td>nvarchar(MAX)</td></tr>
<tr><td>NewValue</td><td>New Entity object value</td><td>nvarchar(MAX)</td></tr>
<tr><td>ReferenceTableName</td><td>Name of the reference table</td><td>varchar(50)</td></tr>
</table>
