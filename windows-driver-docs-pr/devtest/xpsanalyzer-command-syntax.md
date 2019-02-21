---
title: XpsAnalyzer 命令语法
description: 若要运行 XpsAnalyzer，请在命令行使用以下语法和参数键入命令。
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
ms.openlocfilehash: fc2bab8bdba1fdd7cfb202b6f93514e83625fe36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534061"
---
# <a name="xpsanalyzer-command-syntax"></a>XpsAnalyzer 命令语法


若要运行 XpsAnalyzer，请在命令行使用以下语法和参数键入命令。

```
    XpsAnalyzer [/XpsFile:FileName] [/Directory:DirectoryName] [/FlushSql:SqlFormat]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________XpsFile_______"></span><span id="________xpsfile_______"></span><span id="________XPSFILE_______"></span> **/XpsFile:**   
指定的路径和要对其进行分析的 XPS 文件的名称。

<span id="________Directory_______"></span><span id="________directory_______"></span><span id="________DIRECTORY_______"></span> **/ 目录：**   
指定的目录，其中包含一个或多个 XPS 文件的路径。

<span id="________FlushSql_______"></span><span id="________flushsql_______"></span><span id="________FLUSHSQL_______"></span> **/FlushSql:**   
配置 SQL 格式创建分析报告，该 XpsAnalyzer 工具。 可以指定以下 SQL 格式：

<span id="SqlServer"></span><span id="sqlserver"></span><span id="SQLSERVER"></span>**SqlServer**  
指定与 Microsoft SQL Server 兼容的格式。

<span id="MySql"></span><span id="mysql"></span><span id="MYSQL"></span>**MySql**  
指定与 MySql 的开源 SQL Server 兼容的格式。

<span id="Oracle"></span><span id="oracle"></span><span id="ORACLE"></span>**Oracle**  
指定与 Oracle SQL Server 兼容的格式。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

时 XpsAnalyzer 分析 XML 文件，会创建包含分析报告的以下两个文件。

<span id="xpsanalyzer_result.htm_______"></span><span id="XPSANALYZER_RESULT.HTM_______"></span>**XpsAnalyzer\_Result.htm**   
超文本标记 (HTM) 格式的 XPS 分析报表。

<span id="xpsanalyzer_result.xml_______"></span><span id="XPSANALYZER_RESULT.XML_______"></span>**XpsAnalyzer\_Result.xml**   
可扩展标记语言 (XML) 格式的 XPS 分析报表。

这些文件中的已分析的 XPS 文件的名称后跟分析报表。

如果 **/目录：** 指定参数，该文件包含驻留在指定的目录中的每个 XPS 文件的分析。 每个文件的名称后跟 XPS 分析该文件。

如果 **/FlushSql:** 指定参数，则 XpsAnalyzer 创建两个 SQL 文件以及 XpsAnalyzer\_Result.htm 和 XpsAnalyzer\_Result.xml 文件。 作为 folllows 是 SQL 文件的详细信息：

<span id="setup_sqlserver.sql_______"></span><span id="SETUP_SQLSERVER.SQL_______"></span>**Setup\_SqlServer.sql**   
此文件包含一个脚本来准备可用于搜索 XPS 分析的 SQL 数据库。

<span id="update_sqlserver.sql_______"></span><span id="UPDATE_SQLSERVER.SQL_______"></span>**Update\_SqlServer.sql**   
此文件包含一个脚本来执行安装程序创建 SQL 数据库中插入 XPS 分析结果\_SqlServer.sql 脚本。

有关 XPS 分析报表的示例，请参阅[XpsAnalyzer 输出](xpsanalyzer-output.md)。









