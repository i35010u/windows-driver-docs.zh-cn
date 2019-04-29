---
title: 系统性资源不足模拟
description: 系统资源不足模拟选项注入资源故障。 内核模式驱动程序中。
ms.assetid: A8351715-8407-4FEF-9050-2F1F2E7FC2FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c11500c180357cff2c74e6aba614a6bbcc8d55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391303"
---
# <a name="systematic-low-resources-simulation"></a>系统性资源不足模拟


系统资源不足模拟选项注入资源故障。 内核模式驱动程序中。 此选项已侵入驱动程序的错误处理路径。 一直很难测试这些路径。 系统资源不足模拟选项以可预测的方式，使它找到可重现问题注入资源故障。 错误路径可轻松地重现，因为它也便于验证这些问题的修补程序。

为了帮助您确定该错误的根本原因，调试器扩展是提供，可以告知用户已插入了完全的失败和以何种顺序。

**谨慎**  此选项不适用于使用当你要验证所有 （或大量的集合） 的计算机上的驱动程序。 仅当你正在单个驱动程序或其附加的筛选器驱动程序的目标测试时，应使用此选项。 在同一时间使用大量的驱动程序在此选项可能会导致不可预知的结果，并可以强制与正在测试驱动程序无关的组件中发生故障。

 

**请注意**  对于 Windows 8.1[基于堆栈的故障注入](stack-based-failure-injection.md)功能，它是 WDK 8 中，已集成到驱动程序验证程序。 在运行 Windows 8.1 的计算机，使用系统资源不足模拟选项。

 

特定驱动程序上启用系统资源不足模拟选项后，它截获对内核和 Ndis.sys 某些调用从该驱动程序。 系统资源不足模拟会查看调用堆栈 — 具体来说，在来自驱动程序启用的调用堆栈的一部分。 如果这是它已见过该堆栈的第一次，操作将失败的调用根据该调用的语义。 否则，如果它已注意到之前调用，它会将它传递通过保持不变。 系统资源不足模拟包含逻辑来处理这一事实可以加载和卸载多次驱动程序。 它将识别即使驱动程序重新加载到不同的内存位置，调用堆栈是相同。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项


可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的系统资源不足模拟功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。 必须重新启动计算机以激活或停用的系统资源不足模拟选项。

-   **在命令行**

    在命令行中，由表示系统资源不足模拟**verifier /flags 0x040000** (位 18)。 对系统资源不足模拟使用 0x040000 标志值，或将 0x040000 添加到标志值。 例如：

    ```
    verifier /flags 0x040000 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    启用系统资源不足模拟选项时，可以使用 **/faultssystematic** *选项*命令行选项以进一步控制系统资源不足模拟。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">选项</th>
    <th align="left">描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>enableboottime</p></td>
    <td align="left"><p>在计算机重新启动后，启用错误注入。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>disableboottime</p></td>
    <td align="left"><p>禁用错误注入在计算机重新启动后 （这是默认设置）。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>recordboottime</p></td>
    <td align="left"><p>启用错误中的注入<em>怎么办</em>模式。 在计算机重启。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>resetboottime</p></td>
    <td align="left"><p>在计算机重新启动后禁用错误注入和清除堆栈的排除列表。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>enableruntime</p></td>
    <td align="left"><p>动态启用故障注入。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>disableruntime</p></td>
    <td align="left"><p>动态禁用错误注入。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>recordruntime</p></td>
    <td align="left"><p>启用动态错误中的注入<em>怎么办</em>模式。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>resetruntime</p></td>
    <td align="left"><p>动态禁用错误注入并清除以前出现故障的堆栈列表。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>querystatistics</p></td>
    <td align="left"><p>显示当前的故障注入统计信息。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>incrementcounter</p></td>
    <td align="left"><p>增量测试通过用于标识时错误被注入的计数器。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>getstackid<em>计数器</em></p></td>
    <td align="left"><p>检索所指示注入堆栈标识符。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>excludestack<em>堆栈 id 为</em></p></td>
    <td align="left"><p>排除故障注入堆栈。</p></td>
    </tr>
    </tbody>
    </table>

     

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中）**系统资源不足模拟**。
    5.  重新启动计算机。

## <a name="span-iddebuggingbugcheckscausedbysystematiclowresourcessimulationspanspan-iddebuggingbugcheckscausedbysystematiclowresourcessimulationspanspan-iddebuggingbugcheckscausedbysystematiclowresourcessimulationspandebugging-bug-checks-caused-by-systematic-low-resources-simulation"></a><span id="Debugging_bug_checks_caused_by_Systematic_low_resources_simulation"></span><span id="debugging_bug_checks_caused_by_systematic_low_resources_simulation"></span><span id="DEBUGGING_BUG_CHECKS_CAUSED_BY_SYSTEMATIC_LOW_RESOURCES_SIMULATION"></span>调试 bug 检查引起的系统资源不足模拟


检查大部分系统资源不足模拟结果与在 bug 中发现的问题。 若要帮助确定这些代码的问题，原因[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)工具为 Windows 8.1 提供调试器扩展 (kdexts.dll) 和必需的符号。

**若要运行的调试程序扩展**

-   在调试器命令提示符下键入以下命令：

    ```
    !verifier 0x800
    ```

这将转储到调试器显示从最新的故障注入的调用堆栈信息。

 

 





