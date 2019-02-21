---
title: 死锁检测
description: 死锁检测
ms.assetid: ecda3e19-218d-484a-973d-8406bed8d820
keywords:
- 死锁检测功能 WDK Driver Verifier
- 死锁 WDK Driver Verifier
- 锁定的资源 WDK Driver Verifier
- 线程锁定 WDK Driver Verifier
ms.date: 07/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: adaf103c38fe11afca2ce8cba65d7c98bc0bde92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526180"
---
# <a name="deadlock-detection"></a>死锁检测


## <span id="ddk_deadlock_detection_tools"></span><span id="DDK_DEADLOCK_DETECTION_TOOLS"></span>


死锁检测监视哪些需要锁定-旋转锁的资源、 互斥体和快速的互斥体的驱动程序的使用。 此驱动程序验证程序选项将检测可能会导致死锁在将来某个时间点的代码逻辑。

驱动程序验证程序的死锁检测选项连同 **！ 死锁**内核调试器扩展是一个有效的工具并确保你的代码可避免这些资源的使用不当。

仅在 Windows XP 和更高版本的 Windows 中支持死锁检测。


### <a name="span-idcausesofdeadlocksspanspan-idcausesofdeadlocksspancauses-of-deadlocks"></a><span id="causes_of_deadlocks"></span><span id="CAUSES_OF_DEADLOCKS"></span>死锁的原因

一个*死锁*两个或多个线程针对某些资源，这样，任何执行有可能会发生冲突时，会出现。

当两个或多个线程等待由另一个线程拥有的资源，最常见形式的死锁时发生。 阐释了这一点，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">线程 1</th>
<th align="left">线程 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>获取一个锁</p></td>
<td align="left"><p>采用锁 B</p></td>
</tr>
<tr class="even">
<td align="left"><p>请求锁 B</p></td>
<td align="left"><p>请求锁的</p></td>
</tr>
</tbody>
</table>

 

如果这两个序列在同一时间，线程 1 将无法获得锁 B 因为归线程 2 和线程 2 将永远不会收到一个锁，因为归线程 1。 充其量，这会导致线程涉及选项可以暂停，并且在最差导致系统停止响应。

死锁并不局限于两个线程和两个资源。 三个线程和三个锁之间的三向死锁的常见-和甚至五个部分或含有 6 部分死锁只会偶尔发生。 这些死锁需要一定的"遗憾的是"因为它们依赖于执行大量操作同时发生的情况。 但是，远锁获得，越有可能，它们将成为。

当一个线程尝试采用已拥有锁时，会发生单线程死锁。

所有死锁共同特征是不遵守锁层次结构。 只要拥有一次获取多个锁，每个锁应具有明确的优先级。 如果 A 是 B 之前一个点和生成 B C 之前在另一个，该层次结构是一个 B。 这意味着，必须从不后仍获取 B 或 C 和 B 必须获取后 c。

即使在没有不可能的死锁，因为维护代码的过程中很容易出现死锁，将会意外地推出时，应遵循锁层次结构。

### <a name="span-idresourcesthatcancausedeadlocksspanspan-idresourcesthatcancausedeadlocksspanresources-that-can-cause-deadlocks"></a><span id="resources_that_can_cause_deadlocks"></span><span id="RESOURCES_THAT_CAN_CAUSE_DEADLOCKS"></span>可能会导致死锁的资源

最明确死锁的结果*拥有*资源。 其中包括自旋锁、 互斥锁、 快速的互斥体和 ERESOURCEs。

发出信号而不是 （如事件和 LPC 端口） 中获取的资源可能会导致更明确的死锁。 当然是可能的也非常常见，代码可以利用这些资源的方式的两个线程最终会无限期地等待彼此完成。 但是，因为这些资源不实际拥有的任何一个线程，不可以拥有任何高的颇有自信地确定拖欠线程。

潜在死锁涉及自旋锁、 互斥体和互斥体，快速查找驱动程序验证程序的死锁检测选项。 它不会监视 ERESOURCEs，使用也不会监视 nonowned 资源的使用。

### <a name="span-ideffectsofdeadlockdetectionspanspan-ideffectsofdeadlockdetectionspaneffects-of-deadlock-detection"></a><span id="effects_of_deadlock_detection"></span><span id="EFFECTS_OF_DEADLOCK_DETECTION"></span>死锁检测的影响

驱动程序验证程序的死锁检测例程查找锁层次结构不一定是同时进行的冲突。 大多数情况下，这些冲突标识时提供的机会，将发生死锁的代码路径。

若要查找潜在的死锁，驱动程序验证程序生成的资源的获得顺序关系图，并检查循环。 如果要创建的每个资源，并绘制一个箭头，在另一部分之前获取任何时间一个锁，路径循环可以代表锁层次结构冲突。

当发现一个这些冲突时，驱动程序验证程序将发出的 bug 检查。 任何实际的死锁发生之前，将发生此情况。

**请注意**  即使冲突的代码路径可以永远不会同时发生，它们应仍如果被重写它们涉及锁层次结构冲突。 此类代码是"死锁发生问题"如果略有重写代码，可能会导致一些实际的死锁。

 

当死锁检测发现违反时，它将发出错误检查 0xC4。 此 bug 检查的第一个参数将指示确切的冲突。 可能的违规包括：

-   在锁层次结构冲突所涉及的两个或多个线程

-   发布顺序不正确的资源

-   尝试获取同一资源两次 （自发生死锁） 的线程

-   发布不具有已获取资源

-   获取它比另一个线程释放资源

-   不止一次初始化或根本未初始化的资源

-   仍然拥有资源的同时删除线程

-   从 Windows 7 开始，Driver Verifier 可预测可能的死锁。 例如，尝试使用相同 KSPIN\_锁数据结构作为常规旋转锁和堆栈排队自旋锁。


请参阅[ **Bug 检查 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (驱动程序\_VERIFIER\_检测到\_冲突) 的 bug 列表检查参数。

### <a name="span-idmonitoringdeadlockdetectionspanspan-idmonitoringdeadlockdetectionspanmonitoring-deadlock-detection"></a><span id="monitoring_deadlock_detection"></span><span id="MONITORING_DEADLOCK_DETECTION"></span>监视死锁检测

死锁检测会发现冲突，一旦 **！ 死锁**内核调试器扩展可用于调查到底已发生了什么。 在最初已获取锁时，它可以显示锁层次结构拓扑，以及每个线程的调用堆栈。

为获得最佳结果，有问题的驱动程序应在上运行已检验版本的 Windows，因为允许内核以获取更完整的运行时堆栈跟踪。

没有的详细的示例[ **！ 死锁**](https://msdn.microsoft.com/library/windows/hardware/ff562326)扩展，以及有关调试器扩展，文档中的 Windows 调试工具软件包的常规信息。 请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)有关详细信息。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的死锁检测功能。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行**

    在命令行中，由表示死锁检测选项**位 5 (0x20)**。 若要激活死锁检测，使用 0x20 标志值，或将 0x20 添加到标志值。 例如：

    ```
    verifier /flags 0x20 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，您可以还激活和停死锁检测用而无需重启计算机，通过添加 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x20 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    死锁检测功能也包含在标准设置。 例如：

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    2.  选择**从完整的列表中选择单个设置**。
    3.  选择 （选中）**死锁检测**。

    死锁检测功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

 

 





