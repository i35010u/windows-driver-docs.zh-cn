---
title: .logappend（追加日志文件）
description: Logpath 命令将事件和命令的副本从调试器命令窗口追加到指定的日志文件。
keywords:
- 将日志文件 ( 追加) 命令
- 日志文件，将日志文件 ( 追加) 命令
- logpath (追加日志文件) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .logappend (Append Log File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed209fffa0965c68d5b2382676bb78ab9296d992
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829809"
---
# <a name="logappend-append-log-file"></a>.logappend（追加日志文件）


**Logpath** 命令将事件和命令的副本从 [调试器命令窗口](debugger-command-window.md)追加到指定的日志文件。

```dbgcmd
.logappend [/u] [FileName]
```

## <a name="span-idddk_meta_append_log_file_dbgspanspan-idddk_meta_append_log_file_dbgspanparameters"></a><span id="ddk_meta_append_log_file_dbg"></span><span id="DDK_META_APPEND_LOG_FILE_DBG"></span>参数


<span id="________u______"></span><span id="________U______"></span>**/u**   
写入 Unicode 格式的日志文件。 如果省略此参数，则调试器会以 ASCII (ANSI) 格式写入日志文件。

**注意**  追加到现有日志文件时，仅当使用 **/u** 选项创建了日志文件时，才应使用 **/u** 参数。 否则，日志文件将包含 ASCII 字符和 Unicode 字符，这可能会导致更难阅读。

 

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*FileName*   
指定日志文件的名称。 可以指定完整路径或仅指定文件名。 如果文件名包含空格，请将 *文件名* 用引号引起来。 如果未指定路径，则调试器将使用当前目录。 如果省略 *FileName*，则调试器会将文件命名为 Dbgeng。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果在运行 **logpath** 命令时已有一个打开的日志文件，则调试器将关闭该日志文件。 如果指定已存在的文件的名称，调试器会将新信息追加到该文件。 如果该文件不存在，调试器将创建该文件。

 

 





