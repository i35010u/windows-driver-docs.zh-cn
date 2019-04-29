---
title: DbgRpc 命令行选项
description: DbgRpc 命令行必须始终包含恰好一个-l，-e，-t、-c，或-a 开关。 遵循这些开关的选项取决于所用的开关。
ms.assetid: 1c90f97c-f054-402d-a559-2459528029b9
keywords:
- DbgRpc 命令行选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbgRpc Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce281a846de1270482ae0e51840c62a388581b0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374924"
---
# <a name="dbgrpc-command-line-options"></a>DbgRpc 命令行选项


DbgRpc 命令行必须始终包含恰好一个-l，-e，-t、-c，或-a 开关。 遵循这些开关的选项取决于所用的开关。 -S、-p 和-r 选项可用于任何其他选项。

```console
 dbgrpc [-s Server -p ProtSeq] [-r Radix] -l -P ProcessID -L CellID1.CellID2 

dbgrpc [-s Server -p ProtSeq] [-r Radix] -e [-E EndpointName] 

dbgrpc [-s Server -p ProtSeq] [-r Radix] -t -P ProcessID [-T ThreadID] 

dbgrpc [-s Server -p ProtSeq] [-r Radix] [-c|-a] [-C CallID] [-I IfStart] [-N ProcNum] [-P ProcessID] 

dbgrpc -? 
```

## <a name="span-idddkdbgrpccommandlineoptionsdbgspanspan-idddkdbgrpccommandlineoptionsdbgspanparameters"></a><span id="ddk_dbgrpc_command_line_options_dbg"></span><span id="DDK_DBGRPC_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-s_______Server______"></span><span id="_______-s_______server______"></span><span id="_______-S_______SERVER______"></span> **-s** *Server*   
允许 DbgRpc 若要查看从远程计算机的信息。 服务器名称应前面加反斜杠标记。 有关远程使用 DbgRpc 详细信息，请参阅[使用 DbgRpc 工具](using-the-dbgrpc-tool.md)。

<span id="_______-p_______ProtSeq______"></span><span id="_______-p_______protseq______"></span><span id="_______-P_______PROTSEQ______"></span> **-p** *ProtSeq*   
指定要使用的远程传输。 可能值*ProtSeq*都**ncacn\_ip\_tcp** （TCP 协议） 和**ncacn\_np** （命名管道协议）。 建议使用 TCP 协议。 有关远程使用 DbgRpc 详细信息，请参阅[使用 DbgRpc 工具](using-the-dbgrpc-tool.md)。

<span id="_______-r_______Radix______"></span><span id="_______-r_______radix______"></span><span id="_______-R_______RADIX______"></span> **-r** *Radix*   
指定要用于命令参数的基数。 默认值为 16 为基数。 如果 **-r**参数，它应该放在最前面的行，因为它只会影响在其自身后面列出的参数。 它不会影响 DbgRpc 工具的输出。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
显示指定的单元格的 RPC 状态信息。 有关示例，请参阅[获取 RPC 单元格信息](get-rpc-cell-information.md)。

<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *ProcessID*   
指定的进程 ID (PID) 的过程。 当 **-l**使用选项时，这应该是其服务器包含所需单元格的过程。 当 **-t**使用选项，不应包含所需的线程过程。 当 **-c**或 **-a**正在使用选项，该参数是可选的则它应该拥有想要显示的调用的服务器进程。

<span id="cellid1.cellid2______"></span><span id="CELLID1.CELLID2______"></span>*CellID1*.*CellID2*   
指定要显示的单元格的数量。

<span id="_______-e______"></span><span id="_______-E______"></span> **-e**   
搜索系统的 RPC 终结点信息的状态信息。 有关示例，请参阅[获取的 RPC 终结点信息](get-rpc-endpoint-information.md)。

<span id="_______EndpointName______"></span><span id="_______endpointname______"></span><span id="_______ENDPOINTNAME______"></span> *EndpointName*   
指定要显示的终结点的数量。 如果省略，将显示在系统上的所有进程的终结点。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
搜索线程信息的系统的 RPC 状态信息。 有关示例，请参阅[获取 RPC 线程信息](get-rpc-thread-information.md)。

<span id="_______ThreadID______"></span><span id="_______threadid______"></span><span id="_______THREADID______"></span> *ThreadID*   
指定要显示线程的线程 ID。 如果省略，将显示指定的进程中的所有线程。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
搜索服务器端的系统的 RPC 状态信息的调用 (SCALL) 信息。 有关示例，请参阅[获取的 RPC 调用信息](get-rpc-call-information.md)。

<span id="_______-a______"></span><span id="_______-A______"></span> **-a**   
搜索系统的 RPC 客户端状态信息的调用 (CCALL) 信息。 有关示例，请参阅[获取 RPC 客户端调用信息](get-rpc-client-call-information.md)。 此选项需要完整的 RPC 状态信息。

<span id="_______CallID______"></span><span id="_______callid______"></span><span id="_______CALLID______"></span> *CallID*   
指定调用 id。 此参数是可选的;仅当你想要显示匹配特定的调用将其包含*CallID*值。

<span id="_______IfStart______"></span><span id="_______ifstart______"></span><span id="_______IFSTART______"></span> *IfStart*   
指定接口的全局唯一标识符 (UUID) 的第一个 dword 值上执行调用。 此参数是可选的;仅当你想要显示匹配特定的调用将其包含*IfStart*值。

<span id="_______ProcNum______"></span><span id="_______procnum______"></span><span id="_______PROCNUM______"></span> *ProcNum*   
指定此调用的过程数。 （RPC 运行时按编号的 IDL 文件中的位置标识接口中的单个例程--在界面中的第一个例程是 0，第二个 1，依此类推。）此参数是可选的;仅当你想要显示匹配特定的调用将其包含*ProcNum*值。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试 Microsoft 远程过程调用 (RPC) 的详细信息，请参阅[RPC 调试](rpc-debugging.md)。

 

 





