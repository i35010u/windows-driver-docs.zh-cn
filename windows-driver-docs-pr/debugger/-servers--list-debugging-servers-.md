---
title: .servers（列出调试服务器）
description: Servers 命令列出此调试器已建立的所有调试服务器。
keywords:
- 列出调试服务器 () 命令
- 通过调试器进行远程调试，并 ( server) 命令列出调试服务器
- . 服务器 (列出调试服务器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .servers (List Debugging Servers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 459e0724358f9049677c6d5d19b5c93b8273e1e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802079"
---
# <a name="servers-list-debugging-servers"></a>.servers（列出调试服务器）


**Servers** 命令列出此调试器已建立的所有调试服务器。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试服务器的完整详细信息，请参阅 [通过调试器进行远程调试](remote-debugging-through-the-debugger.md)。

<a name="remarks"></a>备注
-------

**Servers** 命令的输出列出在其上发出此命令的调试器启动的所有调试服务器。 输出的格式为，以便可以将其按原义方式用作-remote 命令行选项的自变量，或将其粘贴到 WinDbg 对话框中。

每个调试服务器都由唯一的 ID 标识。 如果希望终止调试服务器，可以将此 ID 用作 [**endsrv (End 调试服务器)**](-endsrv--end-debugging-server-.md) 命令的参数。

**Servers** 命令不列出调试器的不同实例在此计算机上启动的调试服务器，也不会列出进程服务器或 KD 连接服务器。

 

 





