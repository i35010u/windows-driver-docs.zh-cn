---
title: 系统性资源不足模拟
description: 系统低资源模拟选项注入内核模式驱动程序中的资源故障。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a1d51f55811942cd5e8e0068239f0f7e3fe2cbd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817433"
---
# <a name="systematic-low-resources-simulation"></a>系统性资源不足模拟

>[!Note]
> **从 Windows 10 预览体验版本19042及更高版本开始，此检查已弃用** 系统低资源模拟选项注入内核模式驱动程序中的资源故障。 此选项穿过驱动程序错误处理路径。 过去，测试这些路径是非常困难的。 系统低资源模拟选项以可预测的方式注入资源故障，这会使其发现的问题成为可重现问题。 由于错误路径容易重现，因此还可以轻松验证这些问题的修复。

为了帮助您确定错误的根本原因，提供了一个调试器扩展，它可以准确地告诉您哪些失败已注入并按何种顺序排列。

**警告**  当验证计算机上的所有 (或大量) 驱动程序时，不应使用此选项。 仅当对单独驱动程序或其附加的筛选器驱动程序进行目标测试时，才应使用此选项。 同时对大量驱动程序使用此选项可能会导致不可预知的结果，并会在与你测试)  (的驱动程序无关的组件中强制崩溃。

 

**注意**  对于 Windows 8.1，在 WDK 8 中提供的 [基于堆栈的故障注入](stack-based-failure-injection.md) 功能已集成到驱动程序验证程序中。 在运行 Windows 8.1 的计算机上，使用 "系统低资源" 模拟选项。

 

当在特定的驱动程序上启用系统低资源模拟选项时，它会截获从该驱动程序到内核的某些调用，并 Ndis.sys。 系统资源不足的模拟在调用堆栈中查看调用堆栈，该堆栈来自启用它的驱动程序。 如果这是第一次看到该堆栈，则会根据调用的语义使调用失败。 否则，如果在之前已发现调用，它将通过保持不变。 系统低资源模拟包含用于处理可以多次加载和卸载驱动程序的逻辑。 即使将驱动程序重装到不同的内存位置，它也会识别出调用堆栈是否相同。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活系统资源不足的模拟功能。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。 您必须重新启动计算机以激活或停用系统低资源模拟选项。

-   **在命令行中**

    在命令行中，系统低资源模拟由 **verifier/flags 0x040000** (第18位) 表示。 若要进行系统低资源模拟，请使用0x040000 的标志值或将0x040000 添加到标志值。 例如：

    ```
    verifier /flags 0x040000 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    启用系统低资源模拟选项后，可以使用 **/Faultssystematic** *选项* 命令行选项来进一步控制系统低资源模拟。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">OPTION</th>
    <th align="left">描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>enableboottime</p></td>
    <td align="left"><p>在计算机重新启动时启用错误注入。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>disableboottime</p></td>
    <td align="left"><p>禁用跨计算机重启的错误注入 (这是默认设置) 。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>recordboottime</p></td>
    <td align="left"><p>在计算机重新启动 <em>时</em> ，在 "if" 模式下启用错误注入。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>resetboottime</p></td>
    <td align="left"><p>禁用跨计算机重启的错误注入，并清除堆栈排除列表。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>enableruntime</p></td>
    <td align="left"><p>动态启用错误注入。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>disableruntime</p></td>
    <td align="left"><p>动态禁用错误注入。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>recordruntime</p></td>
    <td align="left"><p>在 <em>if</em> 模式下动态启用错误注入。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>resetruntime</p></td>
    <td align="left"><p>动态禁用错误注入，并清除以前出错的堆栈列表。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>querystatistics</p></td>
    <td align="left"><p>显示当前错误注入统计信息。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>incrementcounter</p></td>
    <td align="left"><p>递增用于标识注入错误的时间的测试通过计数器。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>getstackid <em>计数器</em></p></td>
    <td align="left"><p>检索指定的注入堆栈标识符。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>excludestack <em>STACKID</em></p></td>
    <td align="left"><p>从错误注入中排除堆栈。</p></td>
    </tr>
    </tbody>
    </table>

     

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **系统低资源模拟**。
    5.  重新启动计算机。

## <a name="span-iddebugging_bug_checks_caused_by_systematic_low_resources_simulationspanspan-iddebugging_bug_checks_caused_by_systematic_low_resources_simulationspanspan-iddebugging_bug_checks_caused_by_systematic_low_resources_simulationspandebugging-bug-checks-caused-by-systematic-low-resources-simulation"></a><span id="Debugging_bug_checks_caused_by_Systematic_low_resources_simulation"></span><span id="debugging_bug_checks_caused_by_systematic_low_resources_simulation"></span><span id="DEBUGGING_BUG_CHECKS_CAUSED_BY_SYSTEMATIC_LOW_RESOURCES_SIMULATION"></span>调试由系统低资源模拟引起的 bug 检查


在系统低资源模拟情况下发现的大多数问题都会导致 bug 检查。 为帮助确定这些代码 bug 的原因， [Windows 调试](../debugger/index.md) 工具 Windows 8.1 提供调试器扩展 ( # A0) 和必要的符号。

**运行调试器扩展**

-   在调试器命令提示符下，键入以下命令：

    ```
    !verifier 0x800
    ```

这会将信息转储到调试器，并显示来自注入的最新失败的调用堆栈。

 

