---
title: .logappend（追加日志文件）
description: .Logappend 命令将附加事件和调试器命令窗口中指定的日志文件的命令的副本。
ms.assetid: e1c58c34-1fc5-4ec3-bd37-6c7816735aec
keywords:
- 追加日志文件 (.logappend) 命令
- 日志文件，追加日志文件 (.logappend) 命令
- .logappend （追加日志文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .logappend (Append Log File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2355ff00e776403108f1f480b2b04a6965927956
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336180"
---
# <a name="logappend-append-log-file"></a>.logappend（追加日志文件）


**.Logappend**命令将附加事件的副本，并从命令[调试器命令窗口](debugger-command-window.md)到指定的日志文件。

```dbgcmd
.logappend [/u] [FileName]
```

## <a name="span-idddkmetaappendlogfiledbgspanspan-idddkmetaappendlogfiledbgspanparameters"></a><span id="ddk_meta_append_log_file_dbg"></span><span id="DDK_META_APPEND_LOG_FILE_DBG"></span>参数


<span id="________u______"></span><span id="________U______"></span> **/u**   
以 Unicode 格式写入日志文件。 如果省略此参数，则调试器以 ASCII (ANSI) 格式写入日志文件。

**请注意**  时将追加到现有日志文件，应使用 **/u**参数仅当使用创建日志文件 **/u**选项。 否则，日志文件将包含 ASCII 和 Unicode 字符，这可能会使更难以阅读。

 

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
指定日志文件的名称。 您可以指定完整路径或文件名。 如果文件名包含空格，则将*文件名*引号引起来。 如果不指定路径，调试器将使用当前目录。 如果省略*文件名*，调试器命名 Dbgeng.log 的文件。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果已有一个日志文件打开运行时 **.logappend**命令时，调试器将关闭日志文件。 如果指定的名称已存在的文件，调试器将追加到文件的新信息。 如果该文件不存在，则调试器将创建它。

 

 





