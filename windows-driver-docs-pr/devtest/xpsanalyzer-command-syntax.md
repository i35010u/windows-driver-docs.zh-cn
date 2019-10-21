---
title: XpsAnalyzer 命令语法
description: 若要运行 XpsAnalyzer，请使用以下语法和参数在命令行中键入命令。
ms.assetid: f91be3ee-e92a-46c8-ab93-96423a35fd86
keywords:
- XpsAnalyzer 命令语法驱动程序开发工具
topic_type:
- apiref
api_name:
- XpsAnalyzer Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 297c48e55ec4921d7d36cabe875e4af7dbe68dbd
ms.sourcegitcommit: 769630c88bf0abd33f702c1eff9336475d92c0d4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72378616"
---
# <a name="xpsanalyzer-command-syntax"></a>XpsAnalyzer 命令语法


若要运行 XpsAnalyzer，请使用以下语法和参数在命令行中键入命令。

```
    XpsAnalyzer [/XpsFile:FileName] [/Directory:DirectoryName] [/FlushSql:SqlFormat]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________XpsFile_______"></span><span id="________xpsfile_______"></span><span id="________XPSFILE_______"></span> **/XpsFile：**    
指定要分析的 XPS 文件的路径和名称。

<span id="________Directory_______"></span><span id="________directory_______"></span><span id="________DIRECTORY_______"></span> **/目录：**    
指定包含一个或多个 XPS 文件的目录的路径。

<span id="________FlushSql_______"></span><span id="________flushsql_______"></span><span id="________FLUSHSQL_______"></span> **/FlushSql：**    
将 XpsAnalyzer 工具配置为以 SQL 格式创建分析报告。 可以指定以下 SQL 格式：

<span id="SqlServer"></span><span id="sqlserver"></span><span id="SQLSERVER"></span>**SqlServer**  
指定与 Microsoft SQL Server 兼容的格式。

<span id="MySql"></span><span id="mysql"></span><span id="MYSQL"></span>**MySql**  
指定与 MySql 开源 SQL Server 兼容的格式。

<span id="Oracle"></span><span id="oracle"></span><span id="ORACLE"></span>**联手**  
指定与 Oracle SQL Server 兼容的格式。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

当 XpsAnalyzer 分析 XML 文件时，它将创建包含分析报告的以下两个文件。

<span id="xpsanalyzer_result.htm_______"></span><span id="XPSANALYZER_RESULT.HTM_______"></span>**XpsAnalyzer \_Result .htm**    
超文本标记（HTM）格式的 XPS 分析报表。

<span id="xpsanalyzer_result.xml_______"></span><span id="XPSANALYZER_RESULT.XML_______"></span>**XpsAnalyzer \_Result .xml**    
可扩展标记语言（XML）格式的 XPS 分析报表。

在这些文件中，已分析的 XPS 文件的名称后跟分析报告。

如果指定了 **/目录：** 参数，则文件包含对位于指定目录中的每个 XPS 文件的分析。 每个文件的名称后跟该文件的 XPS 分析。

如果指定了 **/FlushSql：** 参数，则 XpsAnalyzer 将创建两个 SQL 文件以及 XpsAnalyzer \_Result .Htm 和 XpsAnalyzer \_Result .xml 文件。 SQL 文件的详细信息如下所示：

<span id="setup_sqlserver.sql_______"></span><span id="SETUP_SQLSERVER.SQL_______"></span>**设置 \_SqlServer .sql**    
此文件包含一个脚本，用于准备可用于在 XPS 分析上搜索的 SQL 数据库。

<span id="update_sqlserver.sql_______"></span><span id="UPDATE_SQLSERVER.SQL_______"></span>**更新 \_SqlServer .sql**    
此文件包含一个脚本，用于将 XPS 分析结果插入通过安装 \_SqlServer .sql 脚本创建的 SQL 数据库。

有关 XPS 分析报表的示例，请参阅[XpsAnalyzer Output](xpsanalyzer-output.md)。









