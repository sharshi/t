---
title: Structured Logs in .NET
date: 2025-03-04
authors: [sharshi]
slug: structured-logs-dotnet
description: >
  Structured Logs in .NET
categories:
  - dotnet
comments: true
---


# Structured Logs in .NET

with regular string interpolation, if you want to find all the logs where AccountId == 244 you have to hope the logs are in a very specific format and you need to search for ('accountid: 244', 'account id = 244', 'accountid = 244' etc...).

With structured logs it breaks out those variables into a structured system that recognizes those variables (like {AccountId}) and extracts them into an easily filterable format.

For example:

In the `RCMBackgroundService` there is a log:
`_logger.LogInformation("Excecuting {ClassName}", className);`

You can find any log, logged with the Variable `ClassName` like this:
```
traces
| where customDimensions.OriginalFormat == "{ClassName}"
```
And specific ones like this:
```
traces
| where customDimensions.ClassName == "TaskUpdateNotificationService"
```
