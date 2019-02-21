---
title: .remote_exit （退出调试客户端）
description: .Remote_exit 命令退出调试客户端，但不会结束调试会话。
ms.assetid: 9e15a842-6864-4ff9-97bc-f6cc8549a422
keywords:
- 退出调试客户端 (.remote_exit) 命令
- 调试器退出调试客户端 (.remote_exit) 命令通过远程调试
- .remote_exit （退出调试客户端） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .remote_exit (Exit Debugging Client)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f19ade2702be6d8b1df22fbe6444458a77fbb3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541958"
---
# <a name="remoteexit-exit-debugging-client"></a>.remote\_退出 （退出调试客户端）


**.Remote\_退出**命令退出调试客户端，但不会结束调试会话。

```dbgcmd
.remote_exit [FinalCommands]
```

## <a name="span-idddkmetaexitdebuggingclientdbgspanspan-idddkmetaexitdebuggingclientdbgspanparameters"></a><span id="ddk_meta_exit_debugging_client_dbg"></span><span id="DDK_META_EXIT_DEBUGGING_CLIENT_DBG"></span>参数


<span id="_______FinalCommands______"></span><span id="_______finalcommands______"></span><span id="_______FINALCOMMANDS______"></span> *FinalCommands*   
指定要传递给调试服务器命令字符串。 应使用分号来分隔多个命令。 这些命令传递给调试服务器和连接就会中断。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

可以使用 **.remote\_退出**命令仅在脚本文件中。 您可以将其 KD 和 CDB，但不能在 WinDbg 中使用它。

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

有关脚本文件的详细信息，请参阅[使用脚本文件](using-script-files.md)。 有关调试客户端和调试服务器的详细信息，请参阅[远程调试通过调试器](remote-debugging-through-the-debugger.md)。

<a name="remarks"></a>备注
-------

如果 KD 或 CDB 直接使用，而不使用脚本中，您可以从调试客户端使用退出[ **CTRL + B** ](ctrl-b--quit-local-debugger-.md)密钥。

您不能退出调试客户端通过在 WinDbg 中执行脚本。

 

 





