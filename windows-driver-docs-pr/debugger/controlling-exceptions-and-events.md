---
title: 控制异常和事件
description: 控制异常和事件
ms.assetid: cc8067f3-07de-4ee2-b028-94f9ac088891
keywords:
- exceptions
- 异常，概述
- 异常，处理
- 活动
- 事件，概述
- 事件，处理
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6035e174ed62143b32ff63dfdd1c9151b807ad45
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252951"
---
# <a name="controlling-exceptions-and-events"></a>控制异常和事件


## <span id="ddk_controlling_exceptions_and_events_dbg"></span><span id="DDK_CONTROLLING_EXCEPTIONS_AND_EVENTS_DBG"></span>


可以通过多种方法在用户模式和内核模式应用程序中捕获和处理异常。 活动调试器、事后调试器或内部错误处理例程都是处理异常的常用方法。

有关这些不同异常处理程序的优先顺序的详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。

当 Microsoft Windows 操作系统允许调试器处理异常时，生成异常的应用程序会 *中断* 调试器。 也就是说，应用程序会停止并且调试器会处于活动状态。 然后，调试器可以通过某种方式处理异常或分析这种情况。 然后，调试器可以结束进程，或让它继续运行。

如果调试器忽略异常并使应用程序继续运行，则操作系统将查找其他异常处理程序，就像没有调试器一样。 如果处理异常，应用程序将继续运行。 但是，如果异常仍未处理，则会向调试器提供另一个机会来处理这种情况。

### <a name="span-idusing_the_debugger_to_analyze_an_exceptionspanspan-idusing_the_debugger_to_analyze_an_exceptionspanusing-the-debugger-to-analyze-an-exception"></a><span id="using_the_debugger_to_analyze_an_exception"></span><span id="USING_THE_DEBUGGER_TO_ANALYZE_AN_EXCEPTION"></span>使用调试器分析异常

当异常或事件中断调试器时，可以使用调试器来检查正在执行的代码和应用程序正在使用的内存。 通过更改应用程序中的特定数量或跳转到不同的点，你可以删除导致此异常的原因。

可以通过发出 [**gh (在处理异常时发出异常) **](gh--go-with-exception-handled-.md) 或 [**gn (中转，但不会) 命令处理异常 **](gn--gn--go-with-exception-not-handled-.md) 来继续执行。

如果在调试器的第二个机会中发出 **gn** 命令来处理异常，则应用程序将结束。

### <a name="span-idkernel_mode_exceptionsspanspan-idkernel_mode_exceptionsspankernel-mode-exceptions"></a><span id="kernel_mode_exceptions"></span><span id="KERNEL_MODE_EXCEPTIONS"></span>内核模式异常

内核模式代码中发生的异常比用户模式异常更严重。 如果未处理内核模式异常，则会发出 [bug 检查](bug-checks--blue-screens-.md) 并停止系统。

对于用户模式例外，如果将内核模式调试器附加到系统，则会在 " *bug 检查" 屏幕* 上通知调试器， (也称为 " *蓝屏*) "。 如果未附加调试器，则会出现 "bug 检查" 屏幕。 在这种情况下，操作系统可能会创建 [故障转储文件](crash-dump-files.md)。

### <a name="span-idcontrolling_exceptions_and_events_from_the_debuggerspanspan-idcontrolling_exceptions_and_events_from_the_debuggerspancontrolling-exceptions-and-events-from-the-debugger"></a><span id="controlling_exceptions_and_events_from_the_debugger"></span><span id="CONTROLLING_EXCEPTIONS_AND_EVENTS_FROM_THE_DEBUGGER"></span>控制调试器中的异常和事件

您可以将调试器配置为以特定方式响应指定的异常和事件。

调试器可以设置每个异常或事件的中断状态：

-   事件发生 ("第一次机会" ) 后，就会立即中断调试器。

-   如果其他错误处理程序有机会响应 ("第二次机会" ) ，事件可能会在中中断。

-   此事件还可以向调试器发送消息，但会继续执行。

-   调试器可以忽略此事件。

调试器还可以设置每个异常和事件的处理状态。 调试器可以将事件视为处理的异常或未经处理的异常。 当然， (不是实际错误的事件不需要任何处理。 ) 

可以通过执行下列操作之一来控制中断状态和处理状态：

-   在[调试器命令窗口](debugger-command-window.md)中使用[**SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)、 **SXD**、 **SXN**或**SXI**命令。

-    (CDB 和 NTSD) 使用[**命令行**](cdb-command-line-options.md)中的 **-x**、 **-xe**、 **-xd**、 **-xn**或 **-xi**选项。

-    (CDB、NTSD 和 KD) 在[Tools.ini](configuring-tools-ini.md)文件中使用**sxe**或**sxd**关键字。

-    (WinDbg 仅) 选择 "**调试**" 菜单上的 "[事件筛选器](debug---event-filters.md)" 以打开 "**事件筛选器**" 对话框，然后选择所需的选项。

**Sx \\ *** 命令、 **-x \\ *** 命令行选项和** \\ sx*** Tools.ini 关键字通常设置指定事件的中断状态。 可以添加 **-h** 选项来改为设置处理状态。

有四种特殊事件代码 (**cc**、 **hc**、 **bpec**和 **ssec**) ，始终指定处理状态而不是中断状态。

可以使用 [**. lastevent (显示上一事件) **](-lastevent--display-last-event-.md) 命令显示最近的异常或事件。

### <a name="span-idcontrolling_break_statusspanspan-idcontrolling_break_statusspancontrolling-break-status"></a><span id="controlling_break_status"></span><span id="CONTROLLING_BREAK_STATUS"></span>控制中断状态

设置异常或事件的中断状态时，可以使用以下选项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">状态名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<strong>SXE</strong> 或 <strong>-xe</strong></td>
<td align="left"><p><strong>分</strong></p>
<p> (<strong>启用</strong>) </p></td>
<td align="left"><p>发生此异常时，目标会立即中断到调试器。 此中断发生在激活任何其他错误处理程序之前。 此方法称为 <em>第一次处理</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<strong>SXD</strong> 或 <strong>-xd</strong></td>
<td align="left"><p><strong>第二次中断</strong></p>
<p> (<strong>禁用</strong>) </p></td>
<td align="left"><p>调试器不会中断此类第一次出现的异常 (，尽管) 显示一条消息。 如果其他错误处理程序无法处理此异常，将停止执行，并将目标中断到调试器中。 此方法称为 " <em>第二次处理</em>"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong>SXN</strong> 或 <strong>-xn</strong></td>
<td align="left"><p><strong>输出</strong></p>
<p> (<strong>通知</strong>) </p></td>
<td align="left"><p>发生此异常时，目标应用程序根本不会中断调试器。 但是，会显示一条消息，告知用户发生此异常。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<strong>SXI</strong> 或 <strong>-xi</strong></td>
<td align="left"><p><strong>忽略</strong></p></td>
<td align="left"><p>发生此异常时，目标应用程序不会中断到调试器中，并且不会显示任何消息。</p></td>
</tr>
</tbody>
</table>

 

如果按下的设置不**会出现异常** \* ，则目标应用程序会在第二次中断后进入调试器。 事件的默认状态在本主题的以下 "事件定义和默认值" 一节中列出。

若要使用 WinDbg 图形界面设置中断状态，"**调试**" 菜单上的[事件筛选器](debug---event-filters.md)从 "**事件筛选器**" 对话框中的列表中选择所需的事件，然后选择 "**已启用**"、"**禁用**"、"**输出**" 或 "**忽略**"。

### <a name="span-idcontrolling_handling_statusspanspan-idcontrolling_handling_statusspancontrolling-handling-status"></a><span id="controlling_handling_status"></span><span id="CONTROLLING_HANDLING_STATUS"></span>控制处理状态

所有事件都被视为未处理，除非使用 [**gh () 命令处理的异常 **](gh--go-with-exception-handled-.md) 。

所有异常都被视为未处理，除非你将[ **sx \\ ** * ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令与 **-h**选项一起使用。

此外， **SX** \* 选项可以配置无效句柄、状态 \_ 断点中断指令和单步例外的处理状态。 此配置 (与中断配置分开。 ) 配置其中断状态时，这些事件分别分别命名为 **ch**、 **bpe**和 **sse**。 在配置其处理状态时，这些事件分别分别命名为 **hc**、 **bpec**和 **ssec**。  (完整的事件列表，请参阅下面的 "事件定义和默认值" 一节。 ) 

您可以 (**cc**) （但不是其中断状态）配置 CTRL + C 事件的处理状态。 如果应用程序收到 CTRL + C 事件，应用程序始终中断到调试器。

当**SX** \* 对**cc**、 **hc**、 **bpec**和**ssec**事件使用 sx 命令时，或在**SX** \* 异常中同时使用 sx 命令和 **-h**选项时，将发生以下操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">状态名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SXE</strong></p></td>
<td align="left"><p><strong>已处理</strong></p></td>
<td align="left"><p>继续执行时，该事件被视为已处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SXD、SXN、SXI</strong></p></td>
<td align="left"><p><strong>未处理</strong></p></td>
<td align="left"><p>继续执行时，该事件被视为未处理。</p></td>
</tr>
</tbody>
</table>

 

若要使用 WinDbg 图形界面设置处理状态，请在 "**调试**" 菜单上选择 "[事件筛选器](debug---event-filters.md)"，从 "**事件筛选器**" 对话框中的列表中选择所需的事件，然后选择 "已**处理**" 或 "**未处理**"。

### <a name="span-idautomatic_commandsspanspan-idautomatic_commandsspanautomatic-commands"></a><span id="automatic_commands"></span><span id="AUTOMATIC_COMMANDS"></span>自动命令

调试器还允许您设置在事件或异常导致调试器中断时自动执行的命令。 可以为第一次中断设置命令字符串，为第二次中断设置命令字符串。 可以在[ **SX \\ ** * ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令或[Debug |事件筛选器](debug---event-filters.md)命令。 每个命令字符串可以包含用分号分隔的多个命令。

不管中断状态如何，都将执行这些命令。 也就是说，如果中断状态为 "忽略"，则仍会执行该命令。 如果中断状态为 "第二次中断"，则在涉及到任何其他异常处理程序之前，第一次发生异常时，将执行第一次命令。 命令字符串可以通过执行命令结束，如 [**g (中转) **](g--go-.md)， [**Gh (with 异常处理) **](gh--go-with-exception-handled-.md)，或 [**Gn (中转，但未处理) 的异常 **](gn--gn--go-with-exception-not-handled-.md)。

### <a name="span-idevent_definitions_and_defaultsspanspan-idevent_definitions_and_defaultsspanevent-definitions-and-defaults"></a><span id="event_definitions_and_defaults"></span><span id="EVENT_DEFINITIONS_AND_DEFAULTS"></span>事件定义和默认值

您可以更改中断状态或处理以下异常的状态。 显示其默认中断状态。

以下例外的默认处理状态始终为 "未处理"。 更改此状态时要格外小心。 如果将此状态更改为 "已处理"，则此类型的所有第一次机会和第二次异常都将被视为已处理，此配置将绕过所有异常处理例程。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件代码</th>
<th align="left">含义</th>
<th align="left">默认中断状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>asrt</strong></p></td>
<td align="left"><p>断言失败</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>av</strong></p></td>
<td align="left"><p>访问冲突</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dm</strong></p></td>
<td align="left"><p>数据未对齐</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dz</strong></p></td>
<td align="left"><p>整数被零除</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>c000008e</strong></p></td>
<td align="left"><p>浮点被零除</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>eh</strong></p></td>
<td align="left"><p>C + + EH 异常</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>gp</strong></p></td>
<td align="left"><p>保护页冲突</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>部分</strong></p></td>
<td align="left"><p>非法指令</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sr-iov</strong></p></td>
<td align="left"><p>整数溢出</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lip</strong></p></td>
<td align="left"><p>页内 i/o 错误</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>isc</strong></p></td>
<td align="left"><p>系统调用无效</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lsq</strong></p></td>
<td align="left"><p>锁定顺序无效</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sbo</strong></p></td>
<td align="left"><p>堆栈缓冲区溢出</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sov</strong></p></td>
<td align="left"><p>堆栈溢出</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>wkd</strong></p></td>
<td align="left"><p>唤醒调试器</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>aph</strong></p></td>
<td align="left"><p>应用程序挂起</p>
<p>如果 Windows 操作系统指示进程已停止响应 (即 <em>挂起</em>) ，则会触发此异常。</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>3c</strong></p></td>
<td align="left"><p>子应用程序终止</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>chhc</strong></p></td>
<td align="left"><p>句柄无效</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>数字</em></p></td>
<td align="left"><p>任何带编号的异常</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
</tbody>
</table>

 

**注意**   通过使用[**ah (断言处理) **](ah--assertion-handling-.md)命令，可以覆盖特定地址的**asrt**中断状态。 **Ch**和**hc**事件代码引用相同的异常。 控制其中断状态时，请使用 **sx \* ch**。 控制其处理状态时，请使用 **sx \* hc**。

 

您可以更改中断状态或处理以下异常的状态。 显示其默认中断状态。

以下例外的默认处理状态始终是 "已处理"。 由于这些异常用于与调试器通信，因此通常不应将其状态更改为 "未处理"。 如果调试器忽略异常，则此状态将导致其他异常处理程序捕获异常。

应用程序可以使用 DBG \_ 命令 \_ 异常 (**dbce**) 与调试器通信。 此异常与断点类似，但你可以在**SX** \* 发生此异常时使用 SX 命令以特定方式进行响应。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件代码</th>
<th align="left">含义</th>
<th align="left">默认中断状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dbce</strong></p></td>
<td align="left"><p>特殊调试器命令异常</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>vcpp</strong></p></td>
<td align="left"><p>特殊 Visual C++ 异常</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>wos</strong></p></td>
<td align="left"><p>WOW64 单步例外</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wob</strong></p></td>
<td align="left"><p>WOW64 断点异常-</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sse<br>ssec</strong></p></td>
<td align="left"><p>单步例外</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bpe<br>bpec</strong></p></td>
<td align="left"><p>断点异常</p></td>
<td align="left"><p>中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cce<br>字幕</strong></p></td>
<td align="left"><p>CTRL + C 或 CTRL + BREAK</p>
<p>如果目标为控制台应用程序，并向其传递 CTRL + C 或 CTRL + BREAK，则会触发此异常。</p></td>
<td align="left"><p>中断</p></td>
</tr>
</tbody>
</table>

 

**注意**   上表中的最后三个异常具有两个不同的事件代码。 控制其中断状态时，请使用 **sse**、 **bpe**和 **cce**。 控制其处理状态时，请使用 **ssec**、 **bpec**和 **cc**。

 

### <a name="span-idthe_following_exceptions_are_useful_when_you_are_debugging_managed_codespanspan-idthe_following_exceptions_are_useful_when_you_are_debugging_managed_codespanspan-idthe_following_exceptions_are_useful_when_you_are_debugging_managed_codespanthe-following-exceptions-are-useful-when-you-are-debugging-managed-code"></a><span id="The_following_exceptions_are_useful_when_you_are_debugging_managed_code."></span><span id="the_following_exceptions_are_useful_when_you_are_debugging_managed_code."></span><span id="THE_FOLLOWING_EXCEPTIONS_ARE_USEFUL_WHEN_YOU_ARE_DEBUGGING_MANAGED_CODE."></span>调试托管代码时，以下例外很有用。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件代码</th>
<th align="left">含义</th>
<th align="left">默认状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>clr</strong></p></td>
<td align="left"><p>公共语言运行时异常</p></td>
<td align="left"><p>第二次中断</p>
<p>未处理</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>clrn</strong></p></td>
<td align="left"><p>公共语言运行时通知异常</p></td>
<td align="left"><p>第二次中断</p>
<p>已处理</p></td>
</tr>
</tbody>
</table>

 

您可以更改以下事件的中断状态。 由于这些事件不是异常，因此它们的处理状态是不相关的。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件代码</th>
<th align="left">含义</th>
<th align="left">默认中断状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ser</strong></p></td>
<td align="left"><p>系统错误</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>cpr.log</strong>[<strong>：</strong><em>Process</em>]</p></td>
<td align="left"><p>进程创建</p>
<p>设置此事件的中断状态仅适用于用户模式调试。 此事件不会在内核模式下发生。</p>
<p>仅当已通过-o<strong><a href="cdb-command-line-options.md" data-raw-source="[command-line option](cdb-command-line-options.md)">命令行选项</a></strong> 或通过 <strong><a href="-childdbg--debug-child-processes-.md" data-raw-source="[.childdbg (Debug Child Processes)](-childdbg--debug-child-processes-.md)">. Childdbg (调试子进程) </a></strong> 命令在 CDB 或 WinDbg 中激活了子进程调试后，才能控制此事件。</p>
<p>进程名称可以包含可选的文件扩展名和星号 (<em>) 或问号 (？ ) 为通配符。 调试器只会记住最新的 <strong>cpr.log</strong> 设置。 不支持单独进程的单独设置。 在 <strong>cpr.log</strong> 和 <em>Process</em>之间包含一个冒号或空格。</p>
<p>如果省略了 <em>进程</em> ，则该设置将应用于任何子进程创建。</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>epr</strong>[<strong>：</strong><em>进程</em>]</p></td>
<td align="left"><p>进程退出</p>
<p>设置此事件的中断状态仅适用于用户模式调试。 此事件不会在内核模式下发生。</p>
<p>仅当已通过-o<strong><a href="cdb-command-line-options.md" data-raw-source="[command-line option](cdb-command-line-options.md)">命令行选项</a></strong> 或通过 <strong><a href="-childdbg--debug-child-processes-.md" data-raw-source="[.childdbg (Debug Child Processes)](-childdbg--debug-child-processes-.md)">. Childdbg (调试子进程) </a></strong> 命令在 CDB 或 WinDbg 中激活了子进程调试后，才能控制此事件。</p>
<p>进程名称可以包含可选的文件扩展名和星号 (</em>) 或问号 (？ ) 为通配符。 调试器只会记住最新的 <strong>epr</strong> 设置。 不支持单独进程的单独设置。 在 <strong>epr</strong> 和 <em>Process</em>之间包含一个冒号或空格。</p>
<p>如果省略 <em>进程</em> ，则该设置将应用于任何子进程退出。</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ct</strong></p></td>
<td align="left"><p>线程创建</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>et</strong></p></td>
<td align="left"><p>线程退出</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ld</strong>[<strong>：</strong><em>Module</em>]</p></td>
<td align="left"><p>加载模块</p>
<p>如果指定 <em>module</em>，则在加载带有此名称的模块时会发生中断。 <em>模块</em> 可以指定模块的名称或地址。 如果使用了名称，则 <em>模块</em> 可能包含各种通配符和说明符。  (有关语法的详细信息，请参阅 <a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>。 ) </p>
<p>调试器只会记住最新的 l<strong>d</strong> 设置。 不支持单独模块的单独设置。 在 <strong>ld</strong> 和 <em>Module</em>之间包含一个冒号或空格。</p>
<p>如果省略 <em>module</em> ，则在加载任何模块时触发事件。</p></td>
<td align="left"><p>输出</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ud</strong>[<strong>：</strong><em>Module</em>]</p></td>
<td align="left"><p>卸载模块</p>
<p>如果指定 <em>module</em>，则在卸载具有此名称的模块或该基址时，将发生中断。 <em>模块</em> 可以指定模块的名称或地址。 如果使用了名称，则 <em>Module</em> 可以是精确名称，也可以是包含通配符。 如果 <em>Module</em> 为确切名称，则会使用当前的调试器模块列表立即将其解析为基址，并将其存储为地址。 如果 <em>Module</em> 包含通配符，则在发生卸载事件时将保留模式字符串以供以后匹配。</p>
<p>在很少的情况下，调试器没有用于卸载事件的名称信息，并且仅与基址匹配。 因此，如果 <em>模块</em> 包含通配符，则调试器无法在此特殊的 unload case 中执行名称匹配，并在卸载任何模块时中断。</p>
<p>调试器只会记住最新的 <strong>ud</strong> 设置。 不支持单独模块的单独设置。 在 <strong>ud</strong> 和 <em>Module</em>之间包含一个冒号或空格。</p>
<p>如果省略 <em>module</em> ，则在加载任何模块时触发事件。</p></td>
<td align="left"><p>输出</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>out</strong>[<strong>：</strong><em>Output</em>]</p></td>
<td align="left"><p>目标应用程序输出</p>
<p>如果指定 <em>output</em>，则仅当收到与指定模式匹配的输出时才会发生中断。 <em>输出</em> 可以包含各种通配符和说明符。  (有关语法的详细信息，请参阅 <a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>) 。但是， <em>输出</em> 不能包含冒号或空格。 匹配时不区分大小写。 在 <strong>out</strong> 和 <em>Output</em>之间包含一个冒号或空格。</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ibp</strong></p></td>
<td align="left"><p>初始断点</p>
<p> (在调试会话开始时以及重新启动目标计算机后发生此事件。 ) </p></td>
<td align="left"><p><strong>在用户模式下：</strong> 分. 可以使用 <strong>-g</strong><a href="command-line-options.md" data-raw-source="[command-line option](command-line-options.md)">命令行选项</a>将此状态更改为 "忽略"。</p>
<p><strong>在内核模式下：</strong> 暂且. 可以通过多种方法将此状态更改为 "已启用"。 有关如何更改此状态的详细信息，请参阅 <a href="crashing-and-rebooting-the-target-computer.md" data-raw-source="[Crashing and Rebooting the Target Computer](crashing-and-rebooting-the-target-computer.md)">崩溃和重新启动目标计算机</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.iml</strong></p></td>
<td align="left"><p>初始模块加载</p>
<p>仅 (内核模式) </p></td>
<td align="left"><p>忽略。 可以通过多种方法将此状态更改为 "中断"。 有关如何更改此状态的详细信息，请参阅 <a href="crashing-and-rebooting-the-target-computer.md" data-raw-source="[Crashing and Rebooting the Target Computer](crashing-and-rebooting-the-target-computer.md)">崩溃和重新启动目标计算机</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





