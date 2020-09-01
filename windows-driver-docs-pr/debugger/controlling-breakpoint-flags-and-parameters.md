---
title: 控制断点标志和参数
description: 控制断点标志和参数
ms.assetid: ed702f01-2a30-4ffb-a804-167cf3b19936
keywords:
- 断点、标志和参数
- DEBUG_BREAK_READ
- DEBUG_BREAK_WRITE
- DEBUG_BREAK_EXECUTE
- DEBUG_BREAK_IO
ms.date: 05/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: f3ea6e6c2caa8f0949040aa4418df9a725d49f27
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207343"
---
# <a name="controlling-breakpoint-flags-and-parameters"></a>控制断点标志和参数


## <span id="controlling_breakpoint_flags_and_parameters"></span><span id="CONTROLLING_BREAKPOINT_FLAGS_AND_PARAMETERS"></span>


可以使用许多方法来确定有关断点的基本信息：

-   [**GetId**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getid) 返回断点 ID。

-   [**GetType**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-gettype) 返回 (软件或处理器) 的断点类型和在其上设置断点的有效处理器的类型。

-   [**GetAdder**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder) 返回添加了断点的客户端。

-   [**GetOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffset) 返回断点的地址。

-   [**GetOffsetExpression**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffsetexpression) 返回指定断点位置的表达式字符串。

除了其位置和断点类型外，断点还具有几个控制其行为的参数。

可以通过各种特定方法控制断点参数。 此外，大多数参数都可以使用 [**GetParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getparameters)在一起查询。

### <a name="span-idbreakpoint_flagsspanspan-idbreakpoint_flagsspanbreakpoint-flags"></a><span id="breakpoint_flags"></span><span id="BREAKPOINT_FLAGS"></span>断点标志

断点标志是一种类型的断点参数。

可以使用 [**GetFlags**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getflags)查询断点标志。 可以通过使用 [**AddFlags**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags)、 [**RemoveFlags**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-removeflags)或 [**SetFlags**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setflags)更改它们。

断点标志构成位域。 可在此位字段中使用的可能标志及其含义如下：

<span id="DEBUG_BREAKPOINT_ENABLED"></span><span id="debug_breakpoint_enabled"></span>调试 \_ 断点 \_ 已启用  
设置此标志后，断点将处于 *启用状态* ，并将具有正常效果。 如果未设置此标志，则将 *禁用* 该断点并且不会产生任何影响。 如果希望暂时停用一个断点，可以删除此标志;然后，在想要重新启用此断点时，可以轻松地添加此标志。

<span id="DEBUG_BREAKPOINT_ADDER_ONLY"></span><span id="debug_breakpoint_adder_only"></span>\_仅调试 \_ 断点 \_  
设置此标志后，断点将是一个 *专用断点*。 此断点仅对添加它的客户端可见。 在这种情况下，其他客户端将无法查询该断点的引擎，该引擎将不会向其他客户端发送断点生成的事件。 与此断点相关的所有回调 (事件和 [输出](using-input-and-output.md#output)) 只发送到此客户端。 请参阅 [**GetAdder**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder)。

<span id="DEBUG_BREAKPOINT_GO_ONLY"></span><span id="debug_breakpoint_go_only"></span>调试 \_ 断点 \_ \_ 仅适用于  
设置此标志后，仅当目标处于无限制执行时才会触发断点。 如果引擎正在单步执行目标中的说明，则不会触发此操作。

<span id="DEBUG_BREAKPOINT_ONE_SHOT"></span><span id="debug_breakpoint_one_shot"></span>调试 \_ 断点 \_ 一个 \_ 快照  
设置此标志后，在第一次触发断点时，断点会自动删除。

<span id="DEBUG_BREAKPOINT_DEFERRED"></span><span id="debug_breakpoint_deferred"></span>已 \_ 延迟调试断点 \_  
设置此标志后，断点会 *延迟*。 当使用符号表达式指定断点的偏移量并且引擎无法计算表达式时，引擎将设置此标志。 每当模块加载或 unleaded 在目标中时，引擎将尝试重新计算其位置使用表达式指定的所有断点的表达式。 无法评估的标记将标记为延迟。 任何客户端都不能修改此标志。

### <a name="span-idother_breakpoint_parametersspanspan-idother_breakpoint_parametersspanother-breakpoint-parameters"></a><span id="other_breakpoint_parameters"></span><span id="OTHER_BREAKPOINT_PARAMETERS"></span>其他断点参数

断点参数还包括：

<span id="Pass_count"></span><span id="pass_count"></span><span id="PASS_COUNT"></span>*传递计数*  
如果断点有一个与之关联的传递计数，则在目标已将断点传递到指定次数之前，将不会激活该断点。 最初设置的传递计数可通过使用 [**GetPassCount**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getpasscount)来查找。 在激活之前，引擎将在断点之前传递断点的[**次数。**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getcurrentpasscount) 通过使用 [**SetPassCount**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setpasscount)，可以将传递计数重置为新值。

<span id="Match_thread"></span><span id="match_thread"></span><span id="MATCH_THREAD"></span>*匹配线程*  
如果该断点有一个关联的线程，则在任何其他线程遇到该断点时，它将被其忽略。 可以通过使用 [**GetMatchThreadId**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getmatchthreadid)找到该线程，并且可以使用 [**SetMatchThreadId**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setmatchthreadid)更改该线程。

<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*Command*  
断点可能有一个与之关联的命令。 当断点被激活时，执行该命令。 此命令可通过使用 [**GetCommand**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getcommand)来找到，可以通过使用 [**SetCommand**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setcommand)进行更改。

<span id="Size"></span><span id="size"></span><span id="SIZE"></span>*规格*  
如果该断点是一个处理器断点，则它必须具有指定的大小。 这确定了其访问将激活断点的内存块的大小-块的开头是断点的位置。 可以通过使用 [**GetDataParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)来查找大小，并可使用 [**SetDataParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)进行更改。

<span id="Access_type"></span><span id="access_type"></span><span id="ACCESS_TYPE"></span>*访问类型*  
如果该断点是一个处理器断点，则它必须具有访问类型。 这确定将激活断点的访问类型。 例如，如果目标读取、写入或执行断点指定的内存，则可能会激活断点。 访问类型可以通过使用 [**GetDataParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)来找到，并且可以通过使用 [**SetDataParameters**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)进行更改。

### <a name="span-idvalid_parameters_for_processor_breakpointsspanspan-idvalid_parameters_for_processor_breakpointsspanvalid-parameters-for-processor-breakpoints"></a><span id="valid_parameters_for_processor_breakpoints"></span><span id="VALID_PARAMETERS_FOR_PROCESSOR_BREAKPOINTS"></span>处理器断点的有效参数

以下访问类型适用于处理器断点：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_BREAK_READ</p></td>
<td align="left"><p>当 CPU 读取断点的内存块中的内存时，将触发断点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_WRITE</p></td>
<td align="left"><p>当 CPU 将内存写入断点的内存块时，将触发断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
DEBUG_BREAK_READ |DEBUG_BREAK_WRITE</td>
<td align="left"><p>当 CPU 读取或写入断点的内存块中的内存时，将触发断点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_EXECUTE</p></td>
<td align="left"><p>当 CPU 提取断点的内存块中的指令时，将触发断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_BREAK_IO</p></td>
<td align="left"><p>当访问断点内存块中的 i/o 端口时，将触发断点。 仅 (Windows XP 和 Microsoft Windows Server 2003，仅限内核模式，x86 仅) </p></td>
</tr>
</tbody>
</table>


并非所有的访问类型和大小都在所有处理器上都受支持。 支持以下访问类型和大小：

<span id="x86"></span><span id="X86"></span>x86  
支持所有访问类型。 调试 \_ 中断 \_ 读取的行为类似于调试 \_ 中断 \_ 读取 |调试 \_ 中断 \_ 写入。 大小必须为1、2或4。 断点的地址必须为大小的倍数。

<span id="x64"></span><span id="X64"></span>64  
支持所有访问类型。 调试 \_ 中断 \_ 读取的行为类似于调试 \_ 中断 \_ 读取 |调试 \_ 中断 \_ 写入。 大小必须为1、2、4或8。 断点的地址必须为大小的倍数。