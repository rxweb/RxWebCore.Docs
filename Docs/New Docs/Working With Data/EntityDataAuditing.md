---
title: DataEntityAuditing
author: rxcontributorone
category: newrxwebcore  
---

DataEntityAuditing is done to keep a log of every database change that has been made to the particular entity. 

# AuditRequest

Auditing a server request keeps a track and log of details while any HTTP request is made. It contains information about which user has made request on which application module including its path, method name, timezone and created date.   

> If any unauthenticated user makes request than the user information is not stored.

The following data is stored in AuditRequest 

<table class="table table-bordered table-striped">
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>AuditRequestId</td><td>Id of Audit Request(PK)</td><td>int</td></tr>
<tr><td>TraceIdentifier</td><td>Url of the request</td><td>varchar(50)</td>
</tr><tr><td>KeyId</td><td>Id of entity</td><td>int</td></tr>
<tr><td>CompositeKeyId</td><td>Composite key of the entity</td><td>int</td></tr>
</table>

# AuditRecord

AuditRecord keeps a trace of data of the table on which the operation is done, Its Key and composite key and the type of event which is occured.

The following data is stored in AuditRecord

<table class="table table-bordered table-striped">
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>AuditRecordId</td><td>Id of Audit Record(PK)</td><td>int</td></tr>
<tr><td>AuditRequestId</td><td>Id of Audit Request(FK AuditRequest)</td><td>int</td></tr>
<tr><td>KeyId</td><td>Id of entity</td><td>int</td></tr>
<tr><td>CompositeKeyId</td><td>Composite key of the entity</td><td>int</td>
</tr><tr><td>EventType</td><td>Type of event</td><td>varchar(1)</td></tr>
<tr><td>TableName</td><td>Name of the table on which the operation is done</td><td>varchar(100)</td></tr>
</table>

# AuditRecordDetails

Whenever entity is modified AuditRecordDetails keeps a track and log of information of oldValue, newValue, ColumnName where the updation is done.

The following data is stored in AuditRecordDetails

<table class="table table-bordered table-striped">
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>AuditRecordDetailId</td><td>Id of Audit Record Detail(PK)</td><td>int</td></tr>
<tr><td>AuditRecordId</td><td>Id of Audit RecordId(FK AuditRecord)</td><td>int</td></tr>
<tr><td>ColumnName</td><td>Name of column where data is modified</td><td>varchar(50)</td></tr>
<tr><td>OldValue</td><td>Old Entity object value</td><td>nvarchar(MAX)</td>
</tr><tr><td>NewValue</td><td>New Entity object value</td><td>nvarchar(MAX)</td></tr>
</table>

# Request Traces
Whenever any exception occurs while accessing a api, it stores these information based upon the TraceId(exception and logging reference) 
It stores the value based upon the context that which entity was accessed, when and using which http verb.

<table class="table table-bordered table-striped">
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>TraceId</td><td>Id of Request Traces(PK)</td><td>int</td></tr>
<tr><td>TraceIdentifier</td><td>TraceIdentifier</td><td>varchar(100)</td></tr>
<tr><td>UserId</td><td>Id of the user</td><td>int</td></tr>
<tr><td>TraceType</td><td>Type of the trace</td><td>varchar(200)</td></tr>
<tr><td>Uri</td><td>Url</td><td>varchar(1024)</td></tr>
<tr><td>Verb</td><td>Http verb</td><td>varchar(10)</td></tr>
<tr><td>RequestHeader</td><td>Header of Request</td><td>varchar(max)</td></tr>
<tr><td>StatusCode</td><td>Status code</td><td>int</td></tr>
<tr><td>InTime</td><td>In time of the user</td><td>datetimeoffset(7)</td></tr>
<tr><td>OutTime</td><td>Out time of the user</td><td>datetimeoffset(7)</td></tr>
</table>

# Exception Logs
Details of the exception which occured during the web api call is stored in exception logs.

<table class="table table-bordered table-striped">
<tr><th>ColumnName</th><th>Description</th><th>Type</th></tr>
<tr><td>ExceptionLogId</td><td>Id of Exception Log(PK)</td><td>int</td></tr>
<tr><td>TraceIdentifier</td><td>TraceIdentifier</td><td>varchar(100)</td></tr>
<tr><td>Message</td><td>Message of the exception</td><td>varchar(500)</td></tr>
<tr><td>ExceptionType</td><td>Type of exception</td><td>varchar(200)</td></tr>
<tr><td>ExceptionSource</td><td>Source</td><td>varchar(max)</td></tr>
<tr><td>InnerExceptionMessage</td><td>Inner exception message</td><td>varchar(200)</td></tr>
<tr><td>InnerExceptionStackTrace</td><td>Inner exception stack trace</td><td>varchar(max)</td></tr>
<tr><td>RequestBody</td><td>Body of the request</td><td>varchar(max)</td></tr>
<tr><td>CreatedDate</td><td>Date of the creation</td><td>datetimeoffset(7)</td></tr>
</table>
