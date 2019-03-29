---
title: 控制异常和事件
description: 控制异常和事件
ms.assetid: cc8067f3-07de-4ee2-b028-94f9ac088891
keywords:
- 异常
- 异常概述
- 处理的异常
- 事件
- 事件概述
- 处理的事件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3006c8f18c409208c55e4dad83d33f5f437c88f0
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464353"
---
# <a name="controlling-exceptions-and-events"></a>控制异常和事件


## <span id="ddk_controlling_exceptions_and_events_dbg"></span><span id="DDK_CONTROLLING_EXCEPTIONS_AND_EVENTS_DBG"></span>


您可以捕获并通过多种方法处理在用户模式和内核模式应用程序中的异常。 使用活动的调试器、 事后调试器或一个内部错误处理例程是所有的常见方式处理异常。

有关这些不同的异常处理程序的优先级顺序的详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

Microsoft Windows 操作系统时允许调试器来处理异常，应用程序生成了异常*分解成*调试器。 也就是说，应用程序停止，并且调试器将变为活动状态。 然后，调试器可以某种方式中处理异常或分析这种情况。 调试器可以然后结束该进程或让它继续运行。

如果调试器忽略异常，并让应用程序继续运行，操作系统会查找其他异常处理程序就像没有调试器是存在。 如果处理异常，该应用程序将继续运行。 但是，如果异常保持未处理状态，调试器是然后授予第二个机会处理这种情况。

### <a name="span-idusingthedebuggertoanalyzeanexceptionspanspan-idusingthedebuggertoanalyzeanexceptionspanusing-the-debugger-to-analyze-an-exception"></a><span id="using_the_debugger_to_analyze_an_exception"></span><span id="USING_THE_DEBUGGER_TO_ANALYZE_AN_EXCEPTION"></span>使用调试器分析异常

当事件或异常中断到调试器时，可以使用调试器来检查正在执行的代码和应用程序使用的内存。 通过更改某些数量或跳转到应用程序中的不同点，您可能能够删除异常的原因。

可以通过发出继续执行[ **gh （转到与处理异常）** ](gh--go-with-exception-handled-.md)或[ **gn (Go 与未处理异常)** ](gn--gn--go-with-exception-not-handled-.md)命令。

如果发出**gn**命令，在调试器的第二个机会处理异常，在应用程序结束。

### <a name="span-idkernelmodeexceptionsspanspan-idkernelmodeexceptionsspankernel-mode-exceptions"></a><span id="kernel_mode_exceptions"></span><span id="KERNEL_MODE_EXCEPTIONS"></span>内核模式下的异常

在内核模式代码中发生的异常是用户模式异常比更严重的。 如果未处理内核模式下的异常， [bug 检查](bug-checks--blue-screens-.md)颁发，则系统将停止。

作为用户模式例外情况之外，如果内核模式调试程序附加到系统中，则通知调试器之前*bug 检查屏幕*(也称为*蓝屏*) 显示。 如果未附加调试器，会显示错误检查屏幕。 在这种情况下，操作系统可能会创建[崩溃转储文件](crash-dump-files.md)。

### <a name="span-idcontrollingexceptionsandeventsfromthedebuggerspanspan-idcontrollingexceptionsandeventsfromthedebuggerspancontrolling-exceptions-and-events-from-the-debugger"></a><span id="controlling_exceptions_and_events_from_the_debugger"></span><span id="CONTROLLING_EXCEPTIONS_AND_EVENTS_FROM_THE_DEBUGGER"></span>控制异常和从调试器事件

你可以配置调试器以特定方式对指定的异常和事件做出反应。

调试器可以为每个事件或异常将中断状态设置：

-   事件可以导致调试器中断，一旦它发生 （"第一次机会"）。

-   其他错误处理程序有机会响应 （"第二个机会"） 后，可以中断事件。

-   该事件还可以将调试程序发送一条消息，但继续执行。

-   调试器可以忽略该事件。

调试器还可以设置每个异常和事件的处理状态。 调试器，可以将已处理的异常或未经处理的异常等事件。 （当然，不是实际的错误的事件不需要任何处理。）

通过执行以下任一操作，可以控制中断状态和处理状态：

-   使用[ **SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)， **SXD**， **SXN**，或**SXI**命令[调试器命令窗口](debugger-command-window.md)。

-   （CDB 和 NTSD）使用 **-x**， **-xe**， **-xd**， **-xn**，或 **-xi**选项[ **命令行**](cdb-command-line-options.md)。

-   （CDB、 NTSD 和 KD）使用**sxe**或**sxd**中的关键字[Tools.ini](configuring-tools-ini.md)文件。

-   (仅 WinDbg)单击[事件筛选器](debug---event-filters.md)上**调试**菜单打开**事件筛选器**对话框框中，，然后选择所需的选项。

**SX\\*** 命令， **-x\\*** 命令行选项，以及**sx\\*** Tools.ini 关键字通常情况下设置中断指定事件的状态。 您可以添加 **-h**选项，则要改为设置的处理状态。

有四个特殊的事件代码 (**cc**， **hc**， **bpec**，以及**ssec**)，始终指定而不是中断状态的处理状态。

可通过使用显示的最新的异常或事件[ **.lastevent （显示最后一个事件）** ](-lastevent--display-last-event-.md)命令。

### <a name="span-idcontrollingbreakstatusspanspan-idcontrollingbreakstatusspancontrolling-break-status"></a><span id="controlling_break_status"></span><span id="CONTROLLING_BREAK_STATUS"></span>控制中断状态

当设置的事件或异常中断状态时，可以使用以下选项。

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
<strong>SXE</strong>或<strong>-xe</strong></td>
<td align="left"><p><strong>中断</strong></p>
<p>(<strong>启用</strong>)</p></td>
<td align="left"><p>如果出现此异常，目标立即进入调试器。 在激活任何其他错误处理程序之前，将发生在此中断。 此方法称为<em>首次处理</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<strong>SXD</strong>或<strong>-xd</strong></td>
<td align="left"><p><strong>第二个机会中断</strong></p>
<p>(<strong>禁用</strong>)</p></td>
<td align="left"><p>调试器不会中断此种类型的最可能的异常 （尽管显示一条消息）。 如果其他错误处理程序不能解决此异常，将停止执行，目标会中断到调试器。 此方法称为<em>二次处理</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong>SXN</strong>或<strong>-xn</strong></td>
<td align="left"><p><strong>Output</strong></p>
<p>(<strong>通知</strong>)</p></td>
<td align="left"><p>如果出现此异常，目标应用程序不会中断到调试器根本。 但是，将显示一条消息，告知用户此异常。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<strong>SXI</strong>或<strong>-xi</strong></td>
<td align="left"><p><strong>Ignore</strong></p></td>
<td align="left"><p>如果出现此异常，目标应用程序不会中断到调试器，并不显示任何消息。</p></td>
</tr>
</tbody>
</table>

 

如果异常未预料的**SX** \*目标应用程序设置，进入调试器在第二次机会。 在本主题的"事件定义和默认值"下面列出的事件的默认状态。

若要使用 WinDbg 图形界面，设置中断状态[事件筛选器](debug---event-filters.md)上**调试**菜单中，单击想要从列表中的事件**事件筛选器**对话框框，并选择**已启用**，**禁用**，**输出**，或者**忽略**。

### <a name="span-idcontrollinghandlingstatusspanspan-idcontrollinghandlingstatusspancontrolling-handling-status"></a><span id="controlling_handling_status"></span><span id="CONTROLLING_HANDLING_STATUS"></span>控制处理状态

所有事件都视为未经处理的除非使用[ **gh （转到与处理异常）** ](gh--go-with-exception-handled-.md)命令。

所有异常认为是未经处理的除非使用[ **sx\\**  * ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令一起使用 **-h**选项。

此外， **SX** \*选项可以配置无效句柄，状态的处理状态\_断点中断的说明和单步异常。 （此配置是独立于其中断配置。）在配置其中断状态时，这些事件名为**ch**， **bpe**，并**sse**分别。 在配置它们的处理状态时，这些事件名为**hc**， **bpec**，并**ssec**分别。 （有关事件的完整列表，请参阅以下"事件定义和默认值"部分）。

你可以配置 CTRL + C 事件的处理状态 (**cc**)，但不是中断状态。 如果应用程序收到 CTRL + C 事件时，应用程序始终会中断到调试器。

当你使用**SX** \*命令**抄送**， **hc**， **bpec**，并**ssec**事件，或当你使用**SX** \*命令一起 **-h**选项在出现异常，将执行以下操作。

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
<td align="left"><p><strong>处理</strong></p></td>
<td align="left"><p>该事件被视为已处理时继续执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SXD,SXN,SXI</strong></p></td>
<td align="left"><p><strong>未处理</strong></p></td>
<td align="left"><p>该事件被视为未处理时继续执行。</p></td>
</tr>
</tbody>
</table>

 

若要设置使用 WinDbg 图形界面处理状态，请单击[事件筛选器](debug---event-filters.md)上**调试**菜单中，单击想要从列表中的事件**事件筛选器**对话框中，并选择**Handled**或**未处理**。

### <a name="span-idautomaticcommandsspanspan-idautomaticcommandsspanautomatic-commands"></a><span id="automatic_commands"></span><span id="AUTOMATIC_COMMANDS"></span>自动命令

调试器还可以设置的事件或异常会导致中断到调试器时就会自动执行的命令。 可以设置为最可能发生中断的命令字符串和第二次中断的命令字符串。 可以设置与这些字符串[ **SX\\**  * ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令或[调试 |事件筛选器](debug---event-filters.md)命令。 每个命令字符串可以包含用分号分隔的多个命令。

无论中断状态，则执行这些命令。 也就是说，如果中断状态为"忽略"，是仍会执行该命令。 如果中断状态为"第二次中断"，第一次出现异常后之前所涉及的任何其他异常处理程序, 时执行首次命令。 命令字符串可以如结尾执行命令[ **g （转向）**](g--go-.md)， [ **gh （转到与处理异常）**](gh--go-with-exception-handled-.md)，或[**gn (Go 出现未处理的异常)**](gn--gn--go-with-exception-not-handled-.md)。

### <a name="span-ideventdefinitionsanddefaultsspanspan-ideventdefinitionsanddefaultsspanevent-definitions-and-defaults"></a><span id="event_definitions_and_defaults"></span><span id="EVENT_DEFINITIONS_AND_DEFAULTS"></span>事件定义和默认值

您可以更改中断状态或以下异常的处理状态。 指示其默认中断状态。

处理状态的以下例外的默认值始终为"未处理"。 谨慎更改此状态。 如果此状态更改为"已处理"时，此类型的所有首次和第二次异常都被都视为已处理，并绕过了此配置所有的异常处理例程。

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
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>av</strong></p></td>
<td align="left"><p>访问冲突</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dm</strong></p></td>
<td align="left"><p>数据未对齐</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dz</strong></p></td>
<td align="left"><p>整数被零除</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>c000008e</strong></p></td>
<td align="left"><p>浮点除以零</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>eh</strong></p></td>
<td align="left"><p>C + + EH 异常</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>gp</strong></p></td>
<td align="left"><p>防护页冲突</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ii</strong></p></td>
<td align="left"><p>非法指令</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iov</strong></p></td>
<td align="left"><p>整数溢出</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ip</strong></p></td>
<td align="left"><p>页 I/O 错误</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>isc</strong></p></td>
<td align="left"><p>无效的系统调用</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lsq</strong></p></td>
<td align="left"><p>无效的锁定顺序</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sbo</strong></p></td>
<td align="left"><p>堆栈缓冲区溢出</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sov</strong></p></td>
<td align="left"><p>堆栈溢出</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>wkd</strong></p></td>
<td align="left"><p>唤醒调试器</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>aph</strong></p></td>
<td align="left"><p>应用程序挂起</p>
<p>如果 Windows 操作系统以结束进程已停止响应，则触发此异常 (即<em>挂起</em>)。</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>3c</strong></p></td>
<td align="left"><p>子应用程序终止</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>chhc</strong></p></td>
<td align="left"><p>无效的句柄</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>数量</em></p></td>
<td align="left"><p>带编号的任何异常</p></td>
<td align="left"><p>第二次中断</p></td>
</tr>
</tbody>
</table>

 

**请注意**  您可以重写**asrt**中断特定地址的状态通过使用[ **ah （断言处理）** ](ah--assertion-handling-.md)命令。 **Ch**并**hc**事件代码，请参阅相同的异常。 当正在控制其中断状态时，使用**sx\* ch**。 当正在控制其处理状态时，使用**sx\* hc**。

 

您可以更改中断状态或以下异常的处理状态。 指示其默认中断状态。

以下例外的默认处理状态是始终"处理"。 因为这些异常用于与调试器通信，不应通常更改其状态为"未处理"。 此状态会导致其他异常处理程序捕获的异常，如果调试程序忽略它们。

应用程序可以使用 DBG\_命令\_异常 (**dbce**) 与调试器进行通信。 此异常是类似于一个断点，但可以使用**SX** \*命令后会发生此异常以特定方式做出反应。

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
<td align="left"><p>特殊的调试器命令异常</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>vcpp</strong></p></td>
<td align="left"><p>特殊的 Visual c + + 异常</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>wos</strong></p></td>
<td align="left"><p>WOW64 单步异常</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wob</strong></p></td>
<td align="left"><p>WOW64 断点异常-</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sse<br>ssec</strong></p></td>
<td align="left"><p>单步异常</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bpe<br>bpec</strong></p></td>
<td align="left"><p>断点异常</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cce<br>cc</strong></p></td>
<td align="left"><p>CTRL + C 或 CTRL + BREAK</p>
<p>如果目标是一个控制台应用程序和 CTRL + C 或 CTRL + BREAK 传递给它，则触发此异常。</p></td>
<td align="left"><p>会间休息</p></td>
</tr>
</tbody>
</table>

 

**请注意**  上表中的最后三个异常有两个不同的事件代码。 当正在控制其中断状态时，使用**sse**， **bpe**，并**cce**。 当正在控制它们的处理状态时，使用**ssec**， **bpec**，并**cc**。

 

### <a name="span-idthefollowingexceptionsareusefulwhenyouaredebuggingmanagedcodespanspan-idthefollowingexceptionsareusefulwhenyouaredebuggingmanagedcodespanspan-idthefollowingexceptionsareusefulwhenyouaredebuggingmanagedcodespanthe-following-exceptions-are-useful-when-you-are-debugging-managed-code"></a><span id="The_following_exceptions_are_useful_when_you_are_debugging_managed_code."></span><span id="the_following_exceptions_are_useful_when_you_are_debugging_managed_code."></span><span id="THE_FOLLOWING_EXCEPTIONS_ARE_USEFUL_WHEN_YOU_ARE_DEBUGGING_MANAGED_CODE."></span>调试托管的代码时，以下例外情况非常有用。

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
<p>Handled</p></td>
</tr>
</tbody>
</table>

 

您可以更改以下事件中断状态。 这些事件不是异常，因为它们的处理状态是不相关。

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
<td align="left"><p><strong>cpr</strong>[<strong>:</strong><em>Process</em>]</p></td>
<td align="left"><p>进程创建</p>
<p>此事件将中断状态设置仅适用于用户模式下调试。 在内核模式下不会发生此事件。</p>
<p>您可以控制此事件，仅当你激活 CDB 或 WinDbg 中，通过-o 中的子进程调试<strong><a href="cdb-command-line-options.md" data-raw-source="[command-line option](cdb-command-line-options.md)">命令行选项</a></strong>或通过<strong><a href="-childdbg--debug-child-processes-.md" data-raw-source="[.childdbg (Debug Child Processes)](-childdbg--debug-child-processes-.md)">。（调试子进程） childdbg</a></strong>命令。</p>
<p>进程名称可以包括可选文件扩展名为和一个星号 (<em>) 或问号 （？） 作为通配符。 调试器会记住仅最新<strong>cpr</strong>设置。 不支持单独的进程的单独设置。 包含冒号或之间有空格<strong>cpr</strong>并<em>进程</em>。</p>
<p>如果<em>进程</em>是省略，该设置适用于任何子进程创建。</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>epr</strong>[<strong>:</strong><em>Process</em>]</p></td>
<td align="left"><p>进程退出</p>
<p>此事件将中断状态设置仅适用于用户模式下调试。 在内核模式下不会发生此事件。</p>
<p>您可以控制此事件，仅当你激活 CDB 或 WinDbg 中，通过-o 中的子进程调试<strong><a href="cdb-command-line-options.md" data-raw-source="[command-line option](cdb-command-line-options.md)">命令行选项</a></strong>或通过<strong><a href="-childdbg--debug-child-processes-.md" data-raw-source="[.childdbg (Debug Child Processes)](-childdbg--debug-child-processes-.md)">。（调试子进程） childdbg</a></strong>命令。</p>
<p>进程名称可以包括可选文件扩展名为和一个星号 (</em>) 或问号 （？） 作为通配符。 调试器会记住仅最新<strong>epr</strong>设置。 不支持单独的进程的单独设置。 包含冒号或之间有空格<strong>epr</strong>并<em>进程</em>。</p>
<p>如果<em>进程</em>是省略，该设置适用于任何子进程退出。</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ct</strong></p></td>
<td align="left"><p>创建线程</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>et</strong></p></td>
<td align="left"><p>线程退出时</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ld</strong>[<strong>:</strong><em>模块</em>]</p></td>
<td align="left"><p>负载模块</p>
<p>如果指定<em>模块</em>，具有此名称的模块加载时，将发生中断。 <em>模块</em>可以指定的名称或模块的地址。 如果使用的名称，<em>模块</em>可能包含多个通配符和说明符。 (有关语法的详细信息，请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>。)</p>
<p>调试器会记住仅最新的 l<strong>d</strong>设置。 不支持单独的模块的单独设置。 包含冒号或之间有空格<strong>ld</strong>并<em>模块</em>。</p>
<p>如果<em>模块</em>是省略，都会触发该事件时加载任何模块。</p></td>
<td align="left"><p>输出</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ud</strong>[<strong>:</strong><em>模块</em>]</p></td>
<td align="left"><p>卸载模块</p>
<p>如果指定<em>模块</em>，在中断发生时在卸载模块具有此名称，或在此基址。 <em>模块</em>可以指定的名称或模块的地址。 如果使用的名称，<em>模块</em>可以确切名称或包含通配符。 如果<em>模块</em>是一个确切的名称、 立即解析为一个基址使用当前的调试器模块列表，并且已存储为一个地址。 如果<em>模块</em>包含通配符，为更高版本匹配的卸载事件发生时保留模式字符串。</p>
<p>很少，调试器不具有名为卸载事件的信息，并仅按基地址匹配。 因此，如果<em>模块</em>包含通配符，调试器不能与匹配的名称中执行此特定卸载用例和分页符时在卸载任何模块。</p>
<p>调试器会记住仅最新<strong>ud</strong>设置。 不支持单独的模块的单独设置。 包含冒号或之间有空格<strong>ud</strong>并<em>模块</em>。</p>
<p>如果<em>模块</em>是省略，都会触发该事件时加载任何模块。</p></td>
<td align="left"><p>输出</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>out</strong>[<strong>:</strong><em>Output</em>]</p></td>
<td align="left"><p>目标应用程序输出</p>
<p>如果指定<em>输出</em>，仅当收到与指定的模式匹配的输出时才发生中断。 <em>输出</em>可以包含各种通配符和说明符。 (有关语法的详细信息，请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>。)但是，<em>输出</em>不能包含冒号或空格。 匹配不区分大小写。 包含冒号或之间空格<strong>出</strong>并<em>输出</em>。</p></td>
<td align="left"><p>忽略</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ibp</strong></p></td>
<td align="left"><p>初始断点</p>
<p>（此事件出现和之后重新启动目标计算机的调试会话的开始处。）</p></td>
<td align="left"><p><strong>在用户模式下：</strong>中断。 您可以通过使用此状态更改为"忽略" <strong>-g</strong><a href="command-line-options.md" data-raw-source="[command-line option](command-line-options.md)">命令行选项</a>。</p>
<p><strong>在内核模式下：</strong>忽略。 通过多种方法，可以将此状态更改为"已启用"。 有关如何更改此状态的详细信息，请参阅<a href="crashing-and-rebooting-the-target-computer.md" data-raw-source="[Crashing and Rebooting the Target Computer](crashing-and-rebooting-the-target-computer.md)">崩溃和重新启动目标计算机</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>iml</strong></p></td>
<td align="left"><p>初始模块加载</p>
<p>（仅适用于内核模式）</p></td>
<td align="left"><p>忽略。 通过多种方法，可以将此状态更改为"中断"。 有关如何更改此状态的详细信息，请参阅<a href="crashing-and-rebooting-the-target-computer.md" data-raw-source="[Crashing and Rebooting the Target Computer](crashing-and-rebooting-the-target-computer.md)">崩溃和重新启动目标计算机</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





