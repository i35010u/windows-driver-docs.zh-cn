---
title: 死锁检测
description: 死锁检测
ms.assetid: ecda3e19-218d-484a-973d-8406bed8d820
keywords:
- 死锁检测功能 WDK 驱动程序验证程序
- 死锁 WDK 驱动程序验证程序
- 锁定的资源 WDK 驱动程序验证程序
- 线程锁定 WDK 驱动程序验证程序
ms.date: 07/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: de7979d72bdc6899b51b83eae388d51476b3a690
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999076"
---
# <a name="deadlock-detection"></a>死锁检测


## <span id="ddk_deadlock_detection_tools"></span><span id="DDK_DEADLOCK_DETECTION_TOOLS"></span>


死锁检测会监视驱动程序对需要锁定的资源的使用情况，即自旋锁、互斥体和快速 mutex。 此驱动程序验证程序选项将检测可能会在将来某个点导致死锁的代码逻辑。

驱动程序验证程序的死锁检测选项与 **！死锁**内核调试器扩展一样，是一种有效的工具，可确保代码避免使用这些资源。

只有 Windows XP 和更高版本的 Windows 支持死锁检测。


### <a name="span-idcauses_of_deadlocksspanspan-idcauses_of_deadlocksspancauses-of-deadlocks"></a><span id="causes_of_deadlocks"></span><span id="CAUSES_OF_DEADLOCKS"></span>死锁的原因

当两个或多个线程在某个资源上发生冲突时，就会发生*死锁*，因为这样做可能无法执行。

当两个或多个线程等待另一个线程拥有的资源时，会出现最常见的死锁。 如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">线程1</th>
<th align="left">线程2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>锁定 A</p></td>
<td align="left"><p>采用锁 B</p></td>
</tr>
<tr class="even">
<td align="left"><p>请求锁 B</p></td>
<td align="left"><p>请求锁</p></td>
</tr>
</tbody>
</table>

 

如果同时出现这两个序列，则线程1将永远不会获得锁 B，因为它由线程2拥有，线程2将永远不会获取锁 A，因为它由线程1拥有。 这种情况下，这会导致线程中断，在最坏的情况下导致系统停止响应。

死锁不会限制为两个线程和两个资源。 三个线程和三个锁之间的三向死锁常见--甚至5部分或六部分死锁偶尔发生。 这些死锁需要一定程度的 "糟糕"，因为它们依赖于同时发生的大量事情。 但是，锁获取越多，就越有可能变得越多。

当线程尝试获取已拥有的锁时，可能会发生单线程死锁。

所有死锁之间的常见分母是不遵循锁层次结构。 每当有必要获取多个锁时，每个锁都应具有清晰的优先级。 如果在第一个点之前执行 B，而在另一个位置上进行 b，则层次结构为-B-C。 这意味着不能在 B 或 C 之后获取，而在 C 之后不得获取 B。

即使在维护代码的过程中不会发生死锁，也应遵循锁层次结构，因为在维护代码的过程中，会很容易意外引入死锁。

### <a name="span-idresources_that_can_cause_deadlocksspanspan-idresources_that_can_cause_deadlocksspanresources-that-can-cause-deadlocks"></a><span id="resources_that_can_cause_deadlocks"></span><span id="RESOURCES_THAT_CAN_CAUSE_DEADLOCKS"></span>可能导致死锁的资源

最明确的死锁是*拥有*资源的结果。 其中包括自旋锁、互斥体、快速 mutex 和 ERESOURCEs。

发出信号而不是获得的资源（例如事件和 LPC 端口）往往会导致更不明确的死锁。 当然，对于滥用这些资源的代码而言，这种情况可能是一种可行的，因为这种情况下，两个线程将结束无限期等待完成。 但是，由于这些资源实际上不是任何一个线程所拥有，因此不能在任何程度上确定拖欠线程。

驱动程序验证程序的 "死锁检测" 选项将查找涉及旋转锁、互斥体和快速 mutex 的潜在死锁。 它不会监视 ERESOURCEs 的使用情况，也不会监视 nonowned 资源的使用情况。

### <a name="span-ideffects_of_deadlock_detectionspanspan-ideffects_of_deadlock_detectionspaneffects-of-deadlock-detection"></a><span id="effects_of_deadlock_detection"></span><span id="EFFECTS_OF_DEADLOCK_DETECTION"></span>死锁检测的影响

驱动程序验证程序的死锁检测例程查找不一定同时出现的锁层次结构冲突。 大多数情况下，这些冲突标识在给定机会时将死锁的代码路径。

为了查找潜在的死锁，驱动程序验证程序会生成一个资源获取顺序图形，并检查循环。 如果要为每个资源创建一个节点，并在每次获取一个锁之前绘制一个箭头，则 path 循环会表示锁层次结构冲突。

如果发现其中一个冲突，驱动程序验证程序将发出 bug 检查。 这会在出现任何实际死锁之前发生。

**请注意**   ，即使冲突的代码路径永远无法同时发生，但如果它们涉及到锁层次结构冲突，它们仍应被重写。 此类代码是 "等待发生的死锁"，如果略微重写代码，这可能会导致实际死锁。

 

当死锁检测发现冲突时，它将发出 bug 检查0xC4。 此错误检查的第一个参数将指示具体的冲突。 可能的冲突包括：

-   锁层次结构冲突涉及两个或多个线程

-   按顺序释放的资源

-   尝试获取同一资源两次（自死锁）的线程

-   在未首先获取的情况下发布的资源

-   由不同于获取它的线程发布的资源

-   多次初始化或未初始化的资源

-   在仍拥有资源的情况下删除的线程

-   从 Windows 7 开始，驱动程序验证程序可以预测可能的死锁。 例如，尝试将相同的 KSPIN\_锁数据结构同时用作常规旋转锁和堆栈排队自旋锁。


有关错误检查参数的列表\_，\_请\_参阅[**bug 检查 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) （DRIVER VERIFIER 检测到冲突）。

### <a name="span-idmonitoring_deadlock_detectionspanspan-idmonitoring_deadlock_detectionspanmonitoring-deadlock-detection"></a><span id="monitoring_deadlock_detection"></span><span id="MONITORING_DEADLOCK_DETECTION"></span>监视死锁检测

死锁检测发现冲突后，可使用 **！死锁**内核调试器扩展来准确调查所发生的情况。 它可以显示锁层次结构拓扑以及最初获取锁时每个线程的调用堆栈。

有关详细信息，请参阅 "适用于 Windows 的调试工具" 包中的 "[**死锁**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-deadlock)扩展" 和 "调试器扩展的常规信息"。 有关详细信息，请参阅[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

您可以使用驱动程序验证器管理器或 Verifier 命令行为一个或多个驱动程序激活死锁检测功能。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **在命令行中**

    在命令行中，死锁检测选项以**位5（0x20）** 表示。 若要激活死锁检测，请使用值为0x20 的标志值或将0x20 添加到标志值。 例如：

    ```
    verifier /flags 0x20 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以通过将 **/volatile**参数添加到命令，来激活和停用死锁检测而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x20 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅[使用可变设置](using-volatile-settings.md)。

    "死锁检测" 功能也包含在标准设置中。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证器管理器**

    1.  选择 "**创建自定义设置（对于代码开发人员）** "，然后单击 "**下一步**"。
    2.  选择 "**从完整列表中选择单个设置**"。
    3.  选择（检查）**死锁检测**。

    "死锁检测" 功能也包含在标准设置中。 若要使用此功能，请在驱动程序验证器管理器中单击 "**创建标准设置**"。

 

 





