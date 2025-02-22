---
description: "commit Method (SQLServerXAResource)"
title: "commit Method (SQLServerXAResource) | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ""
ms.technology: connectivity
ms.topic: reference
apiname: 
  - "SQLServerXAResource.commit"
apilocation: 
  - "sqljdbc.jar"
apitype: "Assembly"
ms.assetid: 1d0f8612-fb4a-4eca-bc37-8342e1419fd4
author: David-Engel
ms.author: v-davidengel
---
# commit Method (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Commits the global transaction that is specified by the given Xid object.  
  
## Syntax  
  
```  
  
public void commit(javax.transaction.xa.Xid xid,  
                   boolean onePhase)  
```  
  
#### Parameters  
 *xid*  
  
 An Xid object.  
  
 *onePhase*  
  
 A **boolean** value.  
  
## Exceptions  
 javax.transaction.xa.XAException  
  
## Remarks  
 This commit method is specified by the commit method in the javax.transaction.xa.XAResource interface.  
  
## See Also  
 [SQLServerXAResource Methods](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource Members](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource Class](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
