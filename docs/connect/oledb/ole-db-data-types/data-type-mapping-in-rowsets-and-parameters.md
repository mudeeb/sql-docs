---
title: "Data type mapping in rowsets and parameters (OLE DB driver) | Microsoft Docs"
description: Learn how the OLE DB Driver for SQL Server represents SQL Server data in rowsets and as parameter values, by using the OLE DB defined data types.
ms.custom: ""
ms.date: "02/21/2020"
ms.prod: sql
ms.prod_service: "database-engine, sql-database, synapse-analytics, pdw"
ms.reviewer: ""
ms.technology: connectivity
ms.topic: "reference"
helpviewer_keywords: 
  - "mapping data types [OLE DB]"
  - "DBTYPE_SQLVARIANT data type"
  - "OLE DB Driver for SQL Server, data types"
  - "rowsets [OLE DB], data type mapping"
  - "data types [OLE DB]"
  - "GetColumnInfo function"
  - "parameters [OLE DB]"
  - "SSPROP_ALLOWNATIVEVARIANT property"
  - "GetParameterInfo function"
  - "OLE DB, data types"
author: David-Engel
ms.author: v-davidengel
---
# Data Type Mapping in Rowsets and Parameters
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  In rowsets and as parameter values, the OLE DB Driver for SQL Server represents [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] data by using the following OLE DB defined data types, reported in the functions **IColumnsInfo::GetColumnInfo** and **ICommandWithParameters::GetParameterInfo**.  
  
|SQL Server data type|OLE DB data type|  
|--------------------------|----------------------|  
|**bigint**|DBTYPE_I8|  
|**binary**|DBTYPE_BYTES|  
|**bit**|DBTYPE_BOOL|  
|**char**|DBTYPE_STR|  
|**datetime**|DBTYPE_DBTIMESTAMP|  
|**datetime2**|DBTYPE_DBTIMESTAMP|  
|**decimal**|DBTYPE_NUMERIC|  
|**float**|DBTYPE_R8|  
|**image**|DBTYPE_BYTES|  
|**int**|DBTYPE_I4|  
|**money**|DBTYPE_CY|  
|**nchar**|DBTYPE_WSTR|  
|**ntext**|DBTYPE_WSTR|  
|**numeric**|DBTYPE_NUMERIC|  
|**nvarchar**|DBTYPE_WSTR|  
|**real**|DBTYPE_R4|  
|**smalldatetime**|DBTYPE_DBTIMESTAMP|  
|**smallint**|DBTYPE_I2|  
|**smallmoney**|DBTYPE_CY|  
|**sql_variant**|DBTYPE_VARIANT, DBTYPE_SQLVARIANT|  
|**sysname**|DBTYPE_WSTR|  
|**text**|DBTYPE_STR|  
|**timestamp**|DBTYPE_BYTES|  
|**tinyint**|DBTYPE_UI1|  
|**UDT**|DBTYPE_UDT|  
|**uniqueidentifier**|DBTYPE_GUID|  
|**varbinary**|DBTYPE_BYTES|  
|**varchar**|DBTYPE_STR|  
|**XML**|DBTYPE_XML|  
  
 The OLE DB Driver for SQL Server supports consumer-requested data conversions as shown in the illustration.  
  
 The **sql_variant** objects can hold data of any [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] data type except text, ntext, image, varchar(max), nvarchar(max), varbinary(max), xml, timestamp, and Microsoft .NET Framework common language runtime (CLR) user-defined types. An instance of sql_variant data also cannot have sql_variant as its underlying base data type. For example, the column can contain **smallint** values for some rows, **float** values for other rows, and **char**/**nchar** values in the remainder.  
  
> [!NOTE]  
>  The **sql_variant** data type is similar to the Variant data type in Microsoft Visual Basic® and the DBTYPE_VARIANT, DBTYPE_SQLVARIANT in OLEDB.  
  
 When **sql_variant** data is fetched as DBTYPE_VARIANT, it is put in a VARIANT structure in the buffer. But the subtypes in the VARIANT structure may not map to subtypes defined in the **sql_variant** data type. The **sql_variant** data must then be fetched as DBTYPE_SQLVARIANT in order for all the subtypes to match.  
  
## DBTYPE_SQLVARIANT Data Type  
 To support the **sql_variant** data type, the OLE DB Driver for SQL Server exposes a provider-specific data type called DBTYPE_SQLVARIANT. When **sql_variant** data is fetched in as DBTYPE_SQLVARIANT, it is stored in a provider-specific SSVARIANT structure. The SSVARIANT structure contains all of the subtypes that match the subtypes of the **sql_variant** data type.  
  
 The session property SSPROP_ALLOWNATIVEVARIANT must also be set to TRUE.  
  
## Provider-Specific Property SSPROP_ALLOWNATIVEVARIANT  
 In fetching data, you can specify explicitly what kind of data type should be returned for a column or for a parameter. **IColumnsInfo** can also be used to get the column information and use that to do the binding. When **IColumnsInfo** is used to obtain column information for binding purposes, if the SSPROP_ALLOWNATIVEVARIANT session property is FALSE (default value), DBTYPE_VARIANT is returned for **sql_variant** columns. If SSPROP_ALLOWNATIVEVARIANT property is FALSE DBTYPE_SQLVARIANT is not supported. If SSPROP_ALLOWNATIVEVARIANT property is set to TRUE, the column type is returned as DBTYPE_SQLVARIANT, in which case the buffer will hold the SSVARIANT structure. In fetching **sql_variant** data as DBTYPE_SQLVARIANT, the session property SSPROP_ALLOWNATIVEVARIANT must be set to TRUE.  
  
 SSPROP_ALLOWNATIVEVARIANT property is part of the provider-specific DBPROPSET_SQLSERVERSESSION property set, and is a session property.  
  
 DBTYPE_VARIANT applies to all other OLE DB providers.  
  
## SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT is a session property and is part of DBPROPSET_SQLSERVERSESSION  property set.  
  
|Property|Description|  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|Type: VT_BOOL<br /><br /> R/W: Read/Write<br /><br /> Default: VARIANT_FALSE<br /><br /> Description: Determines if the data fetched in is as DBTYPE_VARIANT or DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: Column type is returned as DBTYPE_SQLVARIANT in which case the buffer will hold SSVARIANT structure.<br /><br /> VARIANT_FALSE: Column type is returned as DBTYPE_VARIANT and the buffer will have VARIANT structure.|  
  
## See Also  
 [Data Types &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
