---
title: DataEntityAuditing
author: rxcontributorone
category: rxwebcore  
---

DataEntityAuditing is done to keep a log of every database change that has been made to the particular entity. 

# AuditRequest

Auditing a server request keeps a track and log of details while any HTTP request is made. It contains information about which user has made request on which application module including its path, method name, timezone and created date.   

> If any unauthenticated user makes request than the user information is not stored.

The following data is stored in AuditRequest 

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| AuditRequestId | Id of Audit Request(PK) | int |
| TraceIdentifier | Url of the request | varchar(50) |
| KeyId | Id of entity | int |
| CompositeKeyId | Composite key of the entity | int |

# AuditRecord

AuditRecord keeps a trace of data of the table on which the operation is done, Its Key and composite key and the type of event which is occured.

The following data is stored in AuditRecord

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| AuditRecordId | Id of Audit Record(PK) | int |
| AuditRequestId | Id of Audit Request(FK AuditRequest) | int |
| KeyId | Id of entity | int |
| CompositeKeyId | Composite key of the entity | int |
| EventType | Type of event | varchar(1) |
| TableName | Name of the table on which the operation is done | varchar(100) |

# AuditRecordDetails

Whenever entity is modified AuditRecordDetails keeps a track and log of information of oldValue, newValue, ColumnName where the updation is done.

The following data is stored in AuditRecordDetails

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| AuditRecordDetailId | Id of Audit Record Detail(PK) | int |
| AuditRecordId | Id of Audit RecordId(FK AuditRecord) | int |
| ColumnName | Name of column where data is modified | varchar(50) |
| OldValue | Old Entity object value | nvarchar(MAX) |
| NewValue | New Entity object value | nvarchar(MAX) |

# Request Traces
Whenever any exception occurs while accessing a api, it stores these information based upon the TraceId(exception and logging reference) 
It stores the value based upon the context that which entity was accessed, when and using which http verb.

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| TraceId | Id of Request Traces(PK) | int |
| TraceIdentifier | TraceIdentifier | varchar(100) |
| UserId | Id of the user | int |
| TraceType | Type of the trace | varchar(10) |
| TraceTitle | Trace Title | varchar(200) |
| Uri | Url | varchar(1024) |
| Verb | Http verb | varchar(10) |
| RequestHeader | Header of Request | varchar(max) |
| ResponseHeader | Header of Request | varchar(max) |
| StatusCode | Status code | int |
| InTime | In time of the user | datetimeoffset(7) |
| OutTime | Out time of the user | datetimeoffset(7) |

# Exception Logs
Details of the exception which occured during the web api call is stored in exception logs.

| ColumnName | Description | Type | 
| ----------- | ----------- | ----------- |
| ExceptionLogId | Id of Exception Log(PK) | int |
| TraceIdentifier | TraceIdentifier | varchar(100) |
| Message | Message of the exception | varchar(500) |
| ExceptionType | Type of exception | varchar(200) |
| ExceptionSource | Source | varchar(max) |
| InnerExceptionMessage | Inner exception message | varchar(200) |
| InnerExceptionStackTrace | Inner exception stack trace | varchar(max) |
| RequestBody | Body of the request | varchar(max) |
| CreatedDate | Date of the creation | datetimeoffset(7) |
