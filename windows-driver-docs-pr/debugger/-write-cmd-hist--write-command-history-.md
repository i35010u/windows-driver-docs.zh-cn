---
title: .write_cmd_hist（写入命令历史记录）
description: .Write_cmd_hist 命令将调试程序命令窗口的整个历史记录写入到一个文件。
ms.assetid: 7d512f0c-56cd-48e5-b618-d5615113f065
keywords:
- .write_cmd_hist （写入命令历史记录） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .write_cmd_hist (Write Command History)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00dd73e25f967e25d6ded22580ae45e5cb6640ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349090"
---
# <a name="writecmdhist-write-command-history"></a>.write\_cmd\_hist （编写命令历史记录）


**.Write\_cmd\_hist**命令将调试程序命令窗口的整个历史记录写入到文件。

```dbgcmd
.write_cmd_hist Filename 
```

## <a name="span-idddkmetacmdhistwritecommandhistorydbgspanspan-idddkmetacmdhistwritecommandhistorydbgspanparameters"></a><span id="ddk_meta_cmd_hist_write_command_history_dbg"></span><span id="DDK_META_CMD_HIST_WRITE_COMMAND_HISTORY_DBG"></span>参数


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *文件名*   
指定的路径和文件名将创建的文件。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅在 WinDbg 中可用，并能在脚本文件。

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

 

 

 





