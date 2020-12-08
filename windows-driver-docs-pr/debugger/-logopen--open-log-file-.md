---
title: .logopen（打开日志文件）
description: Logopen 命令将事件和命令的副本从调试器命令窗口发送到新的日志文件。
keywords:
- 打开日志文件 (. logopen) 命令
- 日志文件，打开日志文件 ( logopen) 命令
- logopen (打开) Windows 调试的日志文件
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .logopen (Open Log File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 470d90adea3f3c59eaa79c10e07b694a6bc9fe4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804023"
---
# <a name="logopen-open-log-file"></a>.logopen（打开日志文件）


**Logopen** 命令将事件和命令的副本从 [调试器命令窗口](debugger-command-window.md)发送到新的日志文件。

```dbgcmd
.logopen [Options] [FileName] 
.logopen /d
```

## <a name="span-idddk_meta_open_log_file_dbgspanspan-idddk_meta_open_log_file_dbgspanparameters"></a><span id="ddk_meta_open_log_file_dbg"></span><span id="DDK_META_OPEN_LOG_FILE_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下任意选项：

<span id="_t"></span><span id="_T"></span>**/t**  
将包含当前日期和时间的进程 ID 追加到日志文件名。 此数据将插入文件名之后和文件扩展名之前。

<span id="_u"></span><span id="_U"></span>**/u**  
写入 Unicode 格式的日志文件。 如果省略此选项，调试器会以 ASCII (ANSI) 格式写入日志文件。

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*FileName*   
指定日志文件的名称。 可以指定完整路径或仅指定文件名。 如果文件名包含空格，请将 *文件名* 用引号引起来。 如果未指定路径，则调试器将使用当前目录。 如果省略 *FileName*，则调试器会将文件命名为 Dbgeng。

<span id="________d______"></span><span id="________D______"></span>**/d**   
根据目标进程或目标计算机的名称以及目标的状态，自动选择文件名。 文件始终具有 .log 文件扩展名。

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

如果在运行 **logopen** 命令时已有一个打开的日志文件，则调试器会将其关闭。 如果指定的文件名已存在，则将覆盖该文件的内容。

**Logopen/t** 命令将进程 ID、日期和时间追加到日志文件名。 在下面的示例中，十六进制形式的进程 ID 为0x02BC，日期为2005年2月28日，时间为9：05：50.935。

```dbgcmd
0:000> .logopen /t c:\logs\mylogfile.txt
Opened log file 'c:\logs\mylogfile_02BC_2005-02-28_09-05-50-935.txt'
```

 

 





