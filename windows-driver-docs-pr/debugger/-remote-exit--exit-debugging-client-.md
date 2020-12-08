---
title: .remote_exit（退出调试客户端）
description: .Remote_exit 命令将退出调试客户端，但不会结束调试会话。
keywords:
- 退出调试客户端 ( .remote_exit) 命令
- 通过调试器进行远程调试，退出调试客户端 ( .remote_exit) 命令
- .remote_exit (退出调试客户端) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .remote_exit (Exit Debugging Client)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b9d72fb3752d1cd9c0ed7a5469e9e837a2cb9bb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795195"
---
# <a name="remote_exit-exit-debugging-client"></a>。远程 \_ 退出 (退出调试客户端) 


**Remote \_ exit** 命令会退出调试客户端，但不会结束调试会话。

```dbgcmd
.remote_exit [FinalCommands]
```

## <a name="span-idddk_meta_exit_debugging_client_dbgspanspan-idddk_meta_exit_debugging_client_dbgspanparameters"></a><span id="ddk_meta_exit_debugging_client_dbg"></span><span id="DDK_META_EXIT_DEBUGGING_CLIENT_DBG"></span>参数


<span id="_______FinalCommands______"></span><span id="_______finalcommands______"></span><span id="_______FINALCOMMANDS______"></span>*FinalCommands*   
指定要传递给调试服务器的命令字符串。 应使用分号分隔多个命令。 这些命令将传递给调试服务器，然后连接将断开。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

只能在脚本文件中使用 **remote \_ exit** 命令。 可以在 KD 和 CDB 中使用它，但不能在 WinDbg 中使用它。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关脚本文件的详细信息，请参阅 [使用脚本文件](using-script-files.md)。 有关调试客户端和调试服务器的详细信息，请参阅 [通过调试器进行远程调试](remote-debugging-through-the-debugger.md)。

<a name="remarks"></a>备注
-------

如果直接使用 KD 或 CDB，而不是使用脚本，则可以使用 [**CTRL + B**](ctrl-b--quit-local-debugger-.md) 键从调试客户端退出。

不能通过在 WinDbg 中执行的脚本退出调试客户端。

 

 





