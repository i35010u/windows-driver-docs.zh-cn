---
title: .servers（列出调试服务器）
description: .Servers 命令将列出已通过此调试器建立的所有调试服务器。
ms.assetid: bf65c6f7-9c59-4756-a667-8b896bd7ea2a
keywords:
- 列出调试服务器 (.servers) 命令
- 通过调试器列出调试服务器 (.servers) 命令的远程调试
- .servers （列表调试服务器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .servers (List Debugging Servers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab582243523d36d9e842f1d910026b6ae3672533
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339775"
---
# <a name="servers-list-debugging-servers"></a>.servers（列出调试服务器）


**.Servers**命令将列出已通过此调试器建立的所有调试服务器。

```dbgcmd
.servers 
```

## <span id="ddk_meta_list_debugging_servers_dbg"></span><span id="DDK_META_LIST_DEBUGGING_SERVERS_DBG"></span>


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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

调试服务器的完整详细信息，请参阅[远程调试通过调试器](remote-debugging-through-the-debugger.md)。

<a name="remarks"></a>备注
-------

输出 **.servers**命令将列出所有调试服务器开始发出此命令时调试器。 设置输出的格式，以便可以作为参数按原义使用的远程命令行选项或粘贴到 WinDbg 对话框。

每个调试服务器标识的唯一 id。 此 ID 可以用作参数[ **.endsrv (结束调试 Server)** ](-endsrv--end-debugging-server-.md)命令时，如果你想要终止调试服务器。

**.Servers**命令不会列出此计算机上启动的调试器，不同实例的调试服务器也不会列出进程服务器或 KD 连接服务器。

 

 





