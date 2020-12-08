---
title: .write_cmd_hist（写入命令历史记录）
description: .Write_cmd_hist 命令将调试器的整个历史记录写入命令窗口文件中。
keywords:
- " (Windows 调试) .write_cmd_hist 写入命令历史记录"
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .write_cmd_hist (Write Command History)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6777fbaa9d04eb3555710e33b9b304e81f26ce3f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819339"
---
# <a name="write_cmd_hist-write-command-history"></a>。编写 \_ cmd \_ 他 (写入命令历史记录) 


**编写 \_ cmd \_ 他** 命令会将调试器的整个历史记录写入文件命令窗口。

```dbgcmd
.write_cmd_hist Filename 
```

## <a name="span-idddk_meta_cmd_hist_write_command_history_dbgspanspan-idddk_meta_cmd_hist_write_command_history_dbgspanparameters"></a><span id="ddk_meta_cmd_hist_write_command_history_dbg"></span><span id="DDK_META_CMD_HIST_WRITE_COMMAND_HISTORY_DBG"></span>参数


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*Filename*   
指定要创建的文件的路径和文件名。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅在 WinDbg 中可用，不能在脚本文件中使用。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

 

 





