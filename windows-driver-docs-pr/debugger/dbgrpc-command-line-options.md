---
title: DbgRpc 命令行选项
description: DbgRpc 命令行必须始终只包含-l、-e、-t、-c 或-a 开关之一。 这些开关后面的选项取决于所使用的开关。
keywords:
- DbgRpc Command-Line 选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbgRpc Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1be8a0988e2430994dc038346d3c28b9207fd3d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833193"
---
# <a name="dbgrpc-command-line-options"></a>DbgRpc 命令行选项


DbgRpc 命令行必须始终只包含-l、-e、-t、-c 或-a 开关之一。 这些开关后面的选项取决于所使用的开关。 -S、-p 和-r 选项可与任何其他选项一起使用。

```console
 dbgrpc [-s Server -p ProtSeq] [-r Radix] -l -P ProcessID -L CellID1.CellID2 

dbgrpc [-s Server -p ProtSeq] [-r Radix] -e [-E EndpointName] 

dbgrpc [-s Server -p ProtSeq] [-r Radix] -t -P ProcessID [-T ThreadID] 

dbgrpc [-s Server -p ProtSeq] [-r Radix] [-c|-a] [-C CallID] [-I IfStart] [-N ProcNum] [-P ProcessID] 

dbgrpc -? 
```

## <a name="span-idddk_dbgrpc_command_line_options_dbgspanspan-idddk_dbgrpc_command_line_options_dbgspanparameters"></a><span id="ddk_dbgrpc_command_line_options_dbg"></span><span id="DDK_DBGRPC_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-s_______Server______"></span><span id="_______-s_______server______"></span><span id="_______-S_______SERVER______"></span>**-s** *服务器*   
允许 DbgRpc 查看来自远程计算机的信息。 服务器名称前面不应带有斜杠标记。 有关远程使用 DbgRpc 的详细信息，请参阅 [使用 DbgRpc 工具](using-the-dbgrpc-tool.md)。

<span id="_______-p_______ProtSeq______"></span><span id="_______-p_______protseq______"></span><span id="_______-P_______PROTSEQ______"></span>**-p** *ProtSeq*   
指定要使用的远程传输。 *ProtSeq* 的可能值为 **ncacn \_ ip \_ tcp** (tcp 协议) 和 **ncacn \_ np** (命名管道协议) 。 建议使用 TCP 协议。 有关远程使用 DbgRpc 的详细信息，请参阅 [使用 DbgRpc 工具](using-the-dbgrpc-tool.md)。

<span id="_______-r_______Radix______"></span><span id="_______-r_______radix______"></span><span id="_______-R_______RADIX______"></span>**-r** *基数*   
指定要用于命令参数的基数。 默认值为16位。 如果使用了 **-r** 参数，则应将其置于行的第一位，因为它只会影响自行列出的参数。 它不会影响 DbgRpc 工具的输出。

<span id="_______-l______"></span><span id="_______-L______"></span>**-l**   
显示指定单元的 RPC 状态信息。 有关示例，请参阅 [获取 RPC 单元信息](get-rpc-cell-information.md)。

<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span>*ProcessID*   
指定进程的进程 ID (PID) 。 当使用 **-l** 选项时，这应该是其服务器包含所需单元格的进程。 当使用 **-t** 选项时，这应该是包含所需线程的进程。 当使用 **-c** 或 **-a** 选项时，此参数是可选的;它应该是拥有要显示的调用的服务器进程。

<span id="cellid1.cellid2______"></span><span id="CELLID1.CELLID2______"></span>*CellID1*。*CellID2*   
指定要显示的单元格的编号。

<span id="_______-e______"></span><span id="_______-E______"></span>**-e**   
在系统的 RPC 状态信息中搜索终结点信息。 有关示例，请参阅 [获取 RPC 终结点信息](get-rpc-endpoint-information.md)。

<span id="_______EndpointName______"></span><span id="_______endpointname______"></span><span id="_______ENDPOINTNAME______"></span>*终结* 点   
指定要显示的终结点的编号。 如果省略，则显示系统上所有进程的终结点。

<span id="_______-t______"></span><span id="_______-T______"></span>**-t**   
在系统的 RPC 状态信息中搜索线程信息。 有关示例，请参阅 [获取 RPC 线程信息](get-rpc-thread-information.md)。

<span id="_______ThreadID______"></span><span id="_______threadid______"></span><span id="_______THREADID______"></span>*ThreadID*   
指定要显示的线程的线程 ID。 如果省略，则将显示指定进程中的所有线程。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
在系统的 RPC 状态信息中搜索服务器端调用 (SCALL) 信息。 有关示例，请参阅 [获取 RPC 调用信息](get-rpc-call-information.md)。

<span id="_______-a______"></span><span id="_______-A______"></span>**-a**   
在系统的 RPC 状态信息中搜索客户端调用 (CCALL) 信息。 有关示例，请参阅 [获取 RPC 客户端调用信息](get-rpc-client-call-information.md)。 此选项需要完整的 RPC 状态信息。

<span id="_______CallID______"></span><span id="_______callid______"></span><span id="_______CALLID______"></span>*CallID*   
指定呼叫 ID。 此参数是可选的;仅当要显示与特定 *CallID* 值匹配的调用时才包括此值。

<span id="_______IfStart______"></span><span id="_______ifstart______"></span><span id="_______IFSTART______"></span>*IfStart*   
指定在其上进行调用 (UUID) 的接口全局唯一标识符的第一个 DWORD。 此参数是可选的;仅当要显示与特定 *IfStart* 值匹配的调用时才包括此值。

<span id="_______ProcNum______"></span><span id="_______procnum______"></span><span id="_______PROCNUM______"></span>*ProcNum*   
指定此调用的过程号。 RPC Run-Time (RPC 通过在 IDL 文件中的位置对其进行编号来标识接口中的各个例程，接口中的第一个例程为0，第二个例程为1，依此类推。 ) 此参数是可选的;仅当要显示与特定 *ProcNum* 值匹配的调用时才包括此值。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试 Microsoft 远程过程调用 (RPC) 的详细信息，请参阅 [Rpc 调试](rpc-debugging.md)。

 

 





