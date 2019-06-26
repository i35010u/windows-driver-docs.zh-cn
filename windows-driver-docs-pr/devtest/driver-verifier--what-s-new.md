---
title: 驱动程序验证程序新增功能
description: 驱动程序验证程序是从 Windows 2000 开始的 Windows 的所有版本中可用。 每个版本引入了新功能，并检查 Windows 驱动程序中查找错误。 本部分汇总了所做的更改，并提供指向相关文档。
ms.assetid: EAC30108-F8A2-4914-9218-2E0672982B7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bd2dd0a08ced9d18b32cab9ea665b61f956d37f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360343"
---
# <a name="driver-verifier-whats-new"></a>驱动程序验证程序：新增功能

[驱动程序验证程序](driver-verifier.md)现已推出 Windows 从 Windows 2000 开始的所有版本。 每个版本引入了新功能，并检查 Windows 驱动程序中查找错误。 本部分汇总了所做的更改，并提供指向相关文档。

* [Windows 10 中的 driver Verifier](#driver-verifier-in-windows10-updated-may-8-2018)
* [Windows 8.1 中的 driver Verifier](#driver-verifier-in-windows-8-1-updated-june-17-2013)
* [Windows 8 中的 driver Verifier](#driver-verifier-in-windows-8-updated-october-20-2012)
* [Windows 7 中的 driver Verifier](#driver-verifier-in-windows-7-updated-october-22-2012)
* [Windows Vista 中的 driver Verifier](#driver-verifier-in-windows-vista-updated-february-9-2009)
* [Windows XP 中的 driver Verifier](#driver-verifier-in-windows-xp-updated-december-4-2001)

## <a name="driver-verifier-in-windows10-updated-may-8-2018"></a>Windows 10 中的 driver Verifier (*更新：2018 年 5 月 8，* )

> [!IMPORTANT]
> 在 Windows 10 1803年之后版本中从开始，运行驱动程序验证程序将不再自动启用 Windows 驱动程序框架 (WDF) 验证。 请注意以下事项：

* 您仍可以启用的驱动程序验证程序的一部分的 WDF 验证`/standard`标志。 请参阅[驱动程序验证工具的命令语法](https://docs.microsoft.com/windows-hardware/drivers/devtest/verifier-command-line)有关详细信息。
* 如果要使用语法启用 DV 此更改会影响您`/flags 0x209BB`WDF 验证不再会自动启用。

从 Windows 10 开始，驱动程序验证程序包括以下技术的新驱动程序验证规则：

* 新的[音频驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
* 新的 [AVStream 驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
* 四个新的 [KMDF 驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
* 三个新的 [NDIS 驱动程序规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

## <a name="driver-verifier-in-windows-8-1-updated-june-17-2013"></a>Windows 8 1 中的 driver Verifier (*更新：2013 年 6 月 17 日*)

从 Windows 8.1 开始，Driver Verifier 引入了四个新选项来检测错误。

* [NDIS/WIFI 验证](ndis-wifi-verification.md)选项适用的 NDIS 和检查之间的 NDIS 微型端口驱动程序和操作系统内核正确交互的无线 LAN 规则集。

* [系统资源不足模拟](systematic-low-resource-simulation.md)选项注入资源故障。 内核模式驱动程序中的。

* [内核同步延迟模糊](kernel-synchronization-delay-fuzzing.md)选项随机排列线程计划，以帮助检测驱动程序中的并发 bug。

* [VM 交换机验证](vm-switch-verification.md)选项可监视筛选器驱动程序 （可扩展交换机扩展） 中运行[HYPER-V 可扩展交换机](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch)。
* 新的调试器扩展： [ **！ ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)

## <a name="driver-verifier-in-windows-8-updated-october-20-2012"></a>Windows 8 中的 driver Verifier (*更新：2012 年 10 月 20 日*)

从 Windows 8 开始，Driver Verifier 引入了五个新选项来检测错误。

* [电源框架延迟模糊](concurrency-stress-test.md)选项插入随机执行延迟，以帮助检测使用电源管理框架 (PoFx) 的驱动程序中的并发 bug。 执行延迟有上限时间限制。 对不直接利用电源管理框架 (PoFx) 的驱动程序不建议使用此选项。
* [DDI 符合性检查](ddi-compliance-checking.md)选项应用相同设备驱动程序接口 (DDI) 用法规则[Static Driver Verifier](static-driver-verifier.md)使用来验证您的驱动程序，可为所需的 IRQL 在函数调用该函数。 作为标准 Driver Verifier 选项的一部分运行 DDI 符合性检查。
* [面向堆栈的固定 MDL 检查](invariant-mdl-checking-for-stack.md)选项用于监控驱动程序如何处理驱动程序堆栈中的固定 MDL 缓冲区。
* [面向驱动程序的固定 MDL 检查](invariant-mdl-checking-for-driver.md)选项用于监控每个驱动程序是如何处理固定 MDL 缓冲区的。
* [基于堆栈的故障注入](stack-based-failure-injection.md)选项注入内核模式驱动程序中的资源分配失败。

当您构建、 部署和测试驱动程序使用 Windows 8 的 WDK 和 Visual Studio 2012 时，还可以配置驱动程序验证程序来部署驱动程序进行测试时测试计算机上运行。

## <a name="driver-verifier-in-windows-7-updated-october-22-2012"></a>Windows 7 中的 driver Verifier (*更新：2012 年 10 月 22 日*)

有关 Windows 7 中已添加的新功能的信息，请参阅白皮书[Windows 7 中的 Driver Verifier]( https://go.microsoft.com/fwlink/p/?linkid=309793)。

适用于 Windows 7 驱动程序验证程序已使用新的测试和功能，可使驱动程序验证程序来公开更多的类的典型驱动程序 bug 得到增强。

* 从内核驱动程序处理对用户的正确引用
* I/O 验证改进
* 特殊池、 池跟踪和低资源模拟改进
* 同步机制的用法不正确
* 不正确的对象的引用
* 从 DPC 例程的池配额费用
* 系统关闭受到阻止或延迟
* 改进了的强制挂起 I/O 请求

在 Windows 7 中，驱动程序验证程序提供了检查排队的自旋锁的这些检查类似于所提供旋转早期 Windows 版本中的锁定。 这些检查包括：

* 验证操作应引发中断请求级别 (IRQL) 值，例如[ **KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))，实际上不降低 IRQL 值。

* 验证该值应小于 IRQL 的操作，如[ **KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)，实际上不引发 IRQL 值。

* 剪裁系统进程的工作集，如果[Force IRQL 检查](force-irql-checking.md)时向调度引发 IRQL 启用选项\_级别或更高版本，以试图公开为可分页内存时可能存在引用驱动程序在提升的 IRQL 运行。

* 如果启用了死锁检测选项是预测可能的死锁。

* 尝试使用相同 KSPIN\_锁数据结构作为旋转锁和堆栈排队自旋锁时已启用死锁检测选项。

* 正在检查的显然不正确的指针值，例如用作数值调节钮锁地址的用户模式虚拟地址。

* 驱动程序验证工具 IRQL 日志中记录的 IRQL 转换。 当你使用时，此信息将出现 **！ verifier 8**的 Windows 调试器扩展。 请参阅[ **！ verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)。

## <a name="additional-debugging-information"></a>其他调试信息

在 Windows 7 中，驱动程序验证程序提供了以下用于调试的其他信息：

按时间顺序对最新的调用中没有的堆栈跟踪日志[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)并[ **KeLeaveCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)从已验证的驱动程序。 使用显示日志内容 **！ verifier 0x200**调试器的 Windows 调试器扩展。 此信息也可用于了解方案在其中一个线程是意外关键区域中运行，或尝试保留已离开临界区。

您可以显示其他信息[强制挂起 I/O 请求](force-pending-i-o-requests.md)通过使用日志 **！ verifier 0x40**调试器扩展。 在早期 Windows 版本，该日志包含 Driver Verifier 强制处于挂起状态的每个 IRP 只是一个堆栈跟踪。 这是从时间的堆栈跟踪时[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)强制挂起的 IRP 的第一次调用。 Windows 7 具有至少两个日志条目，可能会多花大于 2，为每个挂起的 IRP 强制：

* 在驱动程序验证程序时选取 IRP 为采用强制挂起时的堆栈跟踪。 驱动程序验证程序选择的 Irp 为采用强制挂起时的某个已验证的驱动程序调用一些[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。
* 每个堆栈跟踪[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)完成到达已验证的驱动程序之前，为强制 IRP 挂起调用。 多个**IoCompleteRequest**调用可以存在的相同 IRP，因为一个驱动程序可以暂时停止从其完成例程完成，然后将其恢复通过调用**IoCompleteRequest**再次。

IRQL 转换日志中有多个有效的堆栈跟踪。 使用显示此日志 **！ verifier 8**。 在 Windows 7 之前的 Windows 版本中，驱动程序验证程序已尝试记录一些在提升的 IRQL 这些堆栈跟踪，并且无法捕获 IRQL 值较高的堆栈跟踪。 在 Windows 7 中，驱动程序验证程序试图捕获这些堆栈跟踪：

* 然后引发 IRQL，例如，当已验证的驱动程序调用[ **KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)。
* 降低 IRQL 后，当已验证的驱动程序调用[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)。

这样一来，驱动程序验证程序可以捕获多个这些 IRQL 转换堆栈跟踪。

**！ 分析**可以对公开的问题进行分类 （即是在 Windows 7 中的 I/O 验证程序的一部分） 的增强的 I/O 验证程序检查通过。 在早期 Windows 版本，增强的 I/O 验证程序错误报告包括显示驱动程序缺陷已检测到的驱动程序验证程序跟中断到调试器的说明。 运行 **！ 分析**此类中断不会产生有意义的会审的这些分页符许多因为后 **！ 分析**不能使用中出现的错误说明文本中的信息调试器。 在 Windows 7 中，有关这些驱动程序存在的缺陷有意义的信息在内存中保存驱动程序验证程序。 **！ 分析**可以找到此信息并执行得更有意义的自动会审许多这些分页符。

## <a name="driver-verifier-in-windows-vista-updated-february-9-2009"></a>Windows Vista 中的 driver Verifier (*更新：2009 年 2 月 9 日*)

有关 Windows Vista 中已添加的新功能的信息，请参阅白皮书[Windows Vista 中的 Driver Verifier]( https://go.microsoft.com/fwlink/p/?linkid=309794)。

适用于 Windows Vista 驱动程序验证程序已使用新的测试和功能得到增强。

* 启用驱动程序验证程序和更改设置，而无需重新启动
* 增强的资源不足模拟
* 强制挂起 I/O 请求
* 安全检查
* 更全面的 I/O 验证
* 增强的 IRQL 检查
* 其他检查
* 锁定的内存页跟踪
* 其他自动检查

## <a name="driver-verifier-in-windows-xp-updated-december-4-2001"></a>Windows XP 中的 driver Verifier (*更新：2001 年 12 月 4 日*)

驱动程序验证程序是用于监视 Windows 内核模式驱动程序和图形驱动程序的工具。 Microsoft 强烈建议硬件制造商，若要测试其驱动程序与驱动程序验证程序，以确保驱动程序未进行非法的函数调用或引起系统崩溃。 适用于 Microsoft Windows XP，驱动程序验证工具已得到增强与新的测试和功能。

驱动程序提交到 WHQL 测试必须通过驱动程序验证程序。 在 Windows XP 中的新驱动程序验证工具功能包括：

* 驱动程序验证程序管理器，verifier.exe 所有新图形用户界面 (GUI)
* 新自动监视切换堆栈检查
* DMA 验证 （也称为 HAL 验证）、 死锁检测和 SCSI 验证的新驱动程序验证程序选项
* 将"级别 1"和"级别 2"的测试组合的 I/O 验证更改，可选增强的 I/O 验证测试
* 新的调试器扩展[ **！ 死锁**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-deadlock)并[ **！ dma**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-dma)
* 新的 bug 检查：0xE6 (驱动程序\_VERIFIER\_DMA\_冲突) 和 0xF1 (SCSI\_VERIFIER\_检测到\_冲突)
* 其他子代码的现有 bug 检查代码 0xC4 和 0xC9

驱动程序验证工具功能还包括：

* **新的验证程序命令行选项**verifier.exe 实用程序有一个新的参数*VolatileDriverList*，这可以用于 **/adddriver**关键字来指定驱动程序将添加到列表易失性的设置。 *VolatileDriverList*可用于 **/removedriver**关键字来指定要删除的驱动程序列表。
* **新建 ！ verifier 扩展**新建[ **！ verifier** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)扩展其他日志信息显示当监视的资源不足或 IRQL 引发和旋转锁。 联机帮助也是可用的。
  * *标志*0x4 集将导致显示以包括在资源不足模拟期间注入驱动程序验证程序的错误日志
  * *标志*0x8 集将导致显示以包括在正在验证的驱动程序所做的最新的 IRQL 更改日志
  * 如果*标志*等于完全 0x4 或 0x8、 Quantity 参数指定的记录或要包括在显示中的日志条目数
  * **？** 参数显示简短的帮助文本
* **新 ！ gdikdx.verifier 扩展**

    一个新 **！ gdikdx.verifier**扩展名 **！ gdikdx.verifier-s**，有关 GDI 回调函数的列表统计信息在图形驱动程序的资源不足模拟过程中调用。

* 可以在以下两种方式来显示驱动程序验证程序管理器驱动程序验证器管理器的联机帮助的联机帮助：
  * 右键单击驱动程序验证程序管理器窗口中的项，然后选择**这是什么？** 从弹出菜单。
  * 单击问号 ( **？** ) 在窗口的右上角，然后单击驱动程序验证程序管理器窗口中的项。
