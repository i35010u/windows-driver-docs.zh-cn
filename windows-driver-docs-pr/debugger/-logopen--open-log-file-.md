---
title: .logopen（打开日志文件）
description: .Logopen 命令从调试器命令窗口中的事件和命令的一个副本发送到新的日志文件。
ms.assetid: 00ccc09b-3fd7-462f-a688-2f7b45b584fb
keywords:
- 打开日志文件 (.logopen) 命令
- 日志文件中，打开日志文件 (.logopen) 命令
- .logopen （打开日志文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .logopen (Open Log File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06cc9590f1b7304cf1ff5061681d534d5dc87c15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336416"
---
# <a name="logopen-open-log-file"></a>.logopen（打开日志文件）


**.Logopen**命令将发送事件的副本，并从命令[调试器命令窗口](debugger-command-window.md)到新的日志文件。

```dbgcmd
.logopen [Options] [FileName] 
.logopen /d
```

## <a name="span-idddkmetaopenlogfiledbgspanspan-idddkmetaopenlogfiledbgspanparameters"></a><span id="ddk_meta_open_log_file_dbg"></span><span id="DDK_META_OPEN_LOG_FILE_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下任意选项：

<span id="_t"></span><span id="_T"></span>**/t**  
将进程 ID 与当前日期和时间追加到日志文件名称。 之后的文件的名称和文件扩展名之前插入此数据。

<span id="_u"></span><span id="_U"></span>**/u**  
以 Unicode 格式写入日志文件。 如果省略此选项，调试器以 ASCII (ANSI) 格式写入日志文件。

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
指定日志文件的名称。 您可以指定完整路径或文件名。 如果文件名包含空格，则将*文件名*引号引起来。 如果不指定路径，调试器将使用当前目录。 如果省略*文件名*，调试器命名 Dbgeng.log 的文件。

<span id="________d______"></span><span id="________D______"></span> **/d**   
自动选择基于目标进程或目标计算机和目标状态的名称的文件名称。 文件始终具有.log 文件扩展名。

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

如果已有一个日志文件打开运行时 **.logopen**命令时，调试器将其关闭。 如果指定文件名称已存在，将覆盖该文件的内容。

**.Logopen /t**命令将进程 ID、 日期和时间追加到日志文件名称。 在以下示例中，以十六进制格式的进程 ID 是 0x02BC，日期是 2005 年 2 月 28 日，时间是 9:05:50.935。

```dbgcmd
0:000> .logopen /t c:\logs\mylogfile.txt
Opened log file 'c:\logs\mylogfile_02BC_2005-02-28_09-05-50-935.txt'
```

 

 





