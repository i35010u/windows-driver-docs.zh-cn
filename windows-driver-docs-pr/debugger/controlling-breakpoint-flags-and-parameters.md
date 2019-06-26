---
title: 控制断点标志和参数
description: 控制断点标志和参数
ms.assetid: ed702f01-2a30-4ffb-a804-167cf3b19936
keywords:
- 断点、 标志和参数
- DEBUG_BREAK_READ
- DEBUG_BREAK_WRITE
- DEBUG_BREAK_EXECUTE
- DEBUG_BREAK_IO
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6076b76f8db4b8c0f8050fa7730218fb7d60147
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361449"
---
# <a name="controlling-breakpoint-flags-and-parameters"></a>控制断点标志和参数


## <span id="controlling_breakpoint_flags_and_parameters"></span><span id="CONTROLLING_BREAKPOINT_FLAGS_AND_PARAMETERS"></span>


有多种方法可用于确定有关断点的基本信息：

-   [**GetId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getid)返回断点 id。

-   [**GetType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-gettype)返回断点类型 （软件或处理器） 和有效处理器在其设置断点的类型。

-   [**GetAdder** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder)返回添加了断点的客户端。

-   [**GetOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffset)返回断点的地址。

-   [**GetOffsetExpression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffsetexpression)返回指定的断点的位置的表达式字符串。

除了其位置和断点类型，断点具有控制其行为的多个参数。

可以通过各种特定的方法控制断点参数。 此外，大多数参数可能不会查询一起使用[ **GetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getparameters)。

### <a name="span-idbreakpointflagsspanspan-idbreakpointflagsspanbreakpoint-flags"></a><span id="breakpoint_flags"></span><span id="BREAKPOINT_FLAGS"></span>断点标志

断点标志是一种类型的断点参数。

可以使用查询断点标志[ **GetFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getflags)。 可以使用更改[ **AddFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags)， [ **RemoveFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-removeflags)，或[ **SetFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setflags).

断点标志窗体位域。 可在此位字段，以及它们的含义可能标志如下所示：

<span id="DEBUG_BREAKPOINT_ENABLED"></span><span id="debug_breakpoint_enabled"></span>DEBUG\_BREAKPOINT\_ENABLED  
设置此标志，该断点时，*启用*，将其正常起作用。 未设置此标志，该断点时，*禁用*并且不会产生任何影响。 如果你想要暂时停用断点，则可以删除此标志;然后，它很容易添加此标志，当你想要重新启用此断点时。

<span id="DEBUG_BREAKPOINT_ADDER_ONLY"></span><span id="debug_breakpoint_adder_only"></span>调试\_断点\_ADDER\_仅  
设置此标志，该断点时，*专用断点*。 此断点是仅对已添加它的客户端可见。 在这种情况下，其他客户端将不能查询所需断点，引擎和引擎将不会发送给其他客户端断点所生成的事件。 所有的回调 (事件和[输出](using-input-and-output.md#output)) 与此断点将只发送到此客户端。 请参阅[ **GetAdder**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder)。

<span id="DEBUG_BREAKPOINT_GO_ONLY"></span><span id="debug_breakpoint_go_only"></span>调试\_断点\_转\_仅  
设置此标志，如果目标是不受限制的执行过程中，将仅会触发断点。 它不会触发如果引擎逐句通过在目标中的说明。

<span id="DEBUG_BREAKPOINT_ONE_SHOT"></span><span id="debug_breakpoint_one_shot"></span>DEBUG\_BREAKPOINT\_ONE\_SHOT  
当设置此标志时，断点将自动删除本身第一次触发它时。

<span id="DEBUG_BREAKPOINT_DEFERRED"></span><span id="debug_breakpoint_deferred"></span>DEBUG\_BREAKPOINT\_DEFERRED  
设置此标志，该断点时，*延迟*。 使用符号的表达式，指定的断点的偏移量和该引擎无法计算表达式时，将由引擎设置此标志。 每次模块是加载或 unleaded 在目标中，该引擎将尝试重新计算该表达式使用表达式指定其位置的所有断点。 无法计算的那些已标记为延迟。 此标志不能修改任何客户端。

### <a name="span-idotherbreakpointparametersspanspan-idotherbreakpointparametersspanother-breakpoint-parameters"></a><span id="other_breakpoint_parameters"></span><span id="OTHER_BREAKPOINT_PARAMETERS"></span>其他断点参数

断点参数还包括：

<span id="Pass_count"></span><span id="pass_count"></span><span id="PASS_COUNT"></span>*传递计数*  
如果断点有与之关联的传递计数，它不会被激活之前目标已通过断点指定的次数。 可以使用找到最初将设置传递计数[ **GetPassCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getpasscount)。 数的次数的剩余激活它之前，该引擎将通过断点可以找到此[ **GetCurrentPassCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getcurrentpasscount)。 传递计数可以重置为新值通过[ **SetPassCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setpasscount)。

<span id="Match_thread"></span><span id="match_thread"></span><span id="MATCH_THREAD"></span>*匹配线程*  
如果断点有与之关联的线程，它将被忽略由引擎遇到的任何其他线程时。 可以通过使用找到线程[ **GetMatchThreadId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getmatchthreadid)，并可通过使用更改[ **SetMatchThreadId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setmatchthreadid)。

<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*命令*  
断点可能有与之关联的命令。 当断点被激活时，执行该命令。 此命令可通过使用[ **GetCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getcommand)，并可通过使用更改[ **SetCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setcommand)。

<span id="Size"></span><span id="size"></span><span id="SIZE"></span>*大小*  
如果断点处理器断点，它必须具有指定的大小。 这将确定其访问权限将激活该断点的内存块的大小--块的开头是断点的位置。 可以使用找到的大小[ **GetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)，并可通过使用更改[ **SetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)。

<span id="Access_type"></span><span id="access_type"></span><span id="ACCESS_TYPE"></span>*访问类型*  
如果断点处理器断点，它必须具有访问权限类型。 这可确定将激活该断点的访问权限的类型。 例如，如果目标从读取、 写入，或执行由断点指定的内存，可能会激活该断点。 可以使用找到的访问类型[ **GetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)，并可通过使用更改[ **SetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)。

### <a name="span-idvalidparametersforprocessorbreakpointsspanspan-idvalidparametersforprocessorbreakpointsspanvalid-parameters-for-processor-breakpoints"></a><span id="valid_parameters_for_processor_breakpoints"></span><span id="VALID_PARAMETERS_FOR_PROCESSOR_BREAKPOINTS"></span>有效的参数以处理器断点

下面的访问类型可用于为处理器的断点：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_BREAK_READ</p></td>
<td align="left"><p>当 CPU 读取断点的内存块中的内存时，将触发断点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_WRITE</p></td>
<td align="left"><p>CPU 断点的内存块中写入内存时，将触发断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
DEBUG_BREAK_READ | DEBUG_BREAK_WRITE</td>
<td align="left"><p>CPU 读取或写入内存中的断点的内存块时，将触发断点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_EXECUTE</p></td>
<td align="left"><p>CPU 提取断点的内存块中的说明，将触发断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_BREAK_IO</p></td>
<td align="left"><p>访问断点的内存块中的 I/O 端口时，将触发断点。 （Windows XP 和 Microsoft Windows Server 2003 仅限内核仅模式下，仅限 x86）</p></td>
</tr>
</tbody>
</table>

 

所有处理器上支持不是所有的访问类型和大小。 支持下列访问类型和大小：

<span id="x86"></span><span id="X86"></span>x86  
支持所有的访问类型。 调试\_中断\_读取的行为类似于调试\_中断\_读取 |调试\_中断\_编写。 大小必须为 1、 2 或 4。 断点的地址必须是大小的倍数。

<span id="x64"></span><span id="X64"></span>x64  
支持所有的访问类型。 调试\_中断\_读取的行为类似于调试\_中断\_读取 |调试\_中断\_编写。 大小必须为 1、 2、 4 或 8。 断点的地址必须是大小的倍数。

<span id="Itanium"></span><span id="itanium"></span><span id="ITANIUM"></span>Itanium  
所有访问除调试以外的类型\_中断\_支持 IO。 大小必须为的幂;有关调试\_中断\_EXECUTE，大小必须为 16。 断点的地址必须是大小的倍数。

<span id="Itanium_running_in_x86_mode"></span><span id="itanium_running_in_x86_mode"></span><span id="ITANIUM_RUNNING_IN_X86_MODE"></span>Itanium 正在 x86 模式  
与 x86，除非该调试相同\_中断\_IO 不受支持。

 

 





