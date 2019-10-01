---
title: AuditLogs
author: rxcontributorone
category: rxweb core
---

# AuditRequest

Auditing a server request keeps a track and log of details while any HTTP request is made. It contains information about which user has made request on which application module including its path, method name, timezone and created date.   

> If any unauthenticated user makes request than the user information is not stored.

The following data is stored in AuditRequest 

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| AuditRequestId | Id of Audit Request(PK) | int |
| UserId | Id of User(Based upon UserClaim) | int |
| ApplicationModuleId | Id of application module | int |
| MainRecordId | Id of the record | varchar(100) |
| Uri | Http request path | varchar(1024) |
| RequestMethod | request method name | varchar(10) |
| CreatedDate | request creation date | datetime |

# AuditRecord

AuditRecord keeps a track and log of information whenever any data operation is done on any of the entity.

The following data is stored in AuditRecord

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| AuditRecordId | Id of Audit Record(PK) | int |
| AuditRequestId | Id of Audit Request(FK AuditRequest) | int |
| EventTypes | type of operation done | varchar(9) |
| TableName | Name of Table | varchar(50) |
| RecordId | Id of new entity added | varchar(100) |
| RecordName | Name of new entity added | nvarchar(MAX) |

# AuditRecordDetails

Whenever entity is modified AuditRecordDetails keeps a track and log of information of oldValue, newValue, ColumnName and reference table where the updation is done.

The following data is stored in AuditRecordDetails

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| AuditRecordDetailId | Id of Audit Record Detail(PK) | int |
| AuditRecordId | Id of Audit RecordId(FK AuditRecord) | int |
| ColumnName | Name of column where data is modified | varchar(50) |
| OldValue | Old Entity object value | nvarchar(MAX) |
| NewValue | New Entity object value | nvarchar(MAX) |
| ReferenceTableName | Name of the reference table | varchar(50) |