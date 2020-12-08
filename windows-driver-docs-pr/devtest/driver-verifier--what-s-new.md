---
title: 驱动程序验证器新增功能
description: 从 Windows 2000 开始，驱动程序验证器在 Windows 的所有版本中都可用。 每个版本引入了新功能并检查如何在 Windows 驱动程序中查找 bug。 本部分总结了这些更改，并提供相关文档的链接。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fd68d228099c01470d291b03ca4bebf5bb3a5b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839005"
---
# <a name="driver-verifier-whats-new"></a>驱动程序验证程序：新增功能

从 Windows 2000 开始，[驱动程序验证](driver-verifier.md)器在 windows 的所有版本中都可用。 每个版本引入了新功能并检查如何在 Windows 驱动程序中查找 bug。 本部分总结了这些更改，并提供相关文档的链接。

* [Windows 10 中的驱动程序验证程序](#driver-verifier-in-windows10-updated-may-8-2018)
* [Windows 8.1 中的驱动程序验证程序](#driver-verifier-in-windows-8-1-updated-june-17-2013)
* [Windows 8 中的驱动程序验证程序](#driver-verifier-in-windows-8-updated-october-20-2012)
* [Windows 7 中的驱动程序验证程序](#driver-verifier-in-windows-7-updated-october-22-2012)
* [Windows Vista 中的驱动程序验证程序](#driver-verifier-in-windows-vista-updated-february-9-2009)
* [Windows XP 中的驱动程序验证程序](#driver-verifier-in-windows-xp-updated-december-4-2001)

## <a name="driver-verifier-in-windows-10-updated-may-8-2018"></a>Windows 10 中的驱动程序验证程序 (*更新：5月8日 2018*) 

> [!IMPORTANT]
> 从 Windows 10 1803 之后的版本开始，运行驱动程序验证程序将不再自动启用 Windows 驱动程序框架 (WDF) 验证。 请注意以下事项：

* 你仍可以在驱动程序验证程序的标志中启用 WDF 验证 `/standard` 。 有关详细信息，请参阅 [驱动程序验证程序命令语法](./verifier-command-line.md) 。
* 如果你正在启用 DV 语法，则此更改将影响你， `/flags 0x209BB` 因为 WDF 验证将不再自动启用。

从 Windows 10 开始，驱动程序验证器包含适用于以下技术的新驱动程序验证规则：

* 新的[音频驱动程序规则](/windows-hardware/drivers/ddi/index)
* 新的 [AVStream 驱动程序规则](/windows-hardware/drivers/ddi/index)
* 四个新的 [KMDF 驱动程序规则](/windows-hardware/drivers/ddi/index)
* 三个新的 [NDIS 驱动程序规则](/windows-hardware/drivers/ddi/index)

## <a name="driver-verifier-in-windows-8-1-updated-june-17-2013"></a>Windows 8-1 中的驱动程序验证程序 (*更新：6月 17 2013 日*) 

从 Windows 8.1 开始，驱动程序验证程序引入了四个新选项用于检测错误。

* [Ndis/WIFI 验证](ndis-wifi-verification.md)选项应用一组 ndis 和无线 LAN 规则，这些规则检查 ndis 微型端口驱动程序和操作系统内核之间的适当交互。

* [系统低资源模拟](systematic-low-resource-simulation.md)选项注入内核模式驱动程序中的资源故障。

* [内核同步延迟模糊化](kernel-synchronization-delay-fuzzing.md)选项随机化线程计划，以帮助检测驱动程序中的并发 bug。

* [VM 交换机验证](vm-switch-verification.md)选项监视在[hyper-v 可扩展交换机](../network/hyper-v-extensible-switch.md)内运行)  (可扩展交换机扩展的筛选器驱动程序。
* 新调试器扩展： [ **！ ruleinfo**](../debugger/-ruleinfo.md)

## <a name="driver-verifier-in-windows-8-updated-october-20-2012"></a>Windows 8 中的驱动程序验证程序 (*更新：2012年10月20日*) 

从 Windows 8 开始，驱动程序验证程序引入了五个新选项用于检测错误。

* [Power Framework 延迟模糊化](concurrency-stress-test.md)选项可插入随机执行延迟，以帮助检测使用电源管理框架 (PoFx) 的驱动程序中的并发 bug。 执行延迟具有较高的时间限制。 对于不直接利用电源管理框架 (PoFx) 的驱动程序，不建议使用此选项。
* [Ddi 相容性检查](ddi-compliance-checking.md)选项将相同的设备驱动程序接口应用 (DDI) 使用规则，[静态驱动程序验证](static-driver-verifier.md)器使用这些规则来验证驱动程序是否在函数所需的 IRQL 上执行函数调用。 DDI 相容性检查作为标准驱动程序验证程序选项的一部分运行。
* [面向堆栈的固定 MDL 检查](invariant-mdl-checking-for-stack.md)选项用于监控驱动程序如何处理驱动程序堆栈中的固定 MDL 缓冲区。
* [面向驱动程序的固定 MDL 检查](invariant-mdl-checking-for-driver.md)选项用于监控每个驱动程序是如何处理固定 MDL 缓冲区的。
* [基于堆栈的故障注入](stack-based-failure-injection.md)选项注入内核模式驱动程序中的资源分配失败。

使用 Visual Studio 2012 和适用于 Windows 8 的 WDK 构建、部署和测试驱动程序时，还可以将驱动程序验证程序配置为在部署要测试的驱动程序时在测试计算机上运行。

## <a name="driver-verifier-in-windows-7-updated-october-22-2012"></a>Windows 7 中的驱动程序验证程序 (*更新：2012年10月22日*) 

对于 Windows 7，驱动程序验证程序已通过允许驱动程序验证程序公开更多类典型驱动程序错误的新测试和功能进行了增强。

* 来自内核驱动程序的用户句柄引用不正确
* I/o 验证改进
* 特殊池、池跟踪和低资源模拟改进
* 不正确使用同步机制
* 对象引用不正确
* 来自 DPC 例程的池配额费用
* 系统关闭块或延迟
* 改进了强制挂起 i/o 请求

在 Windows 7 中，驱动程序验证程序为排队的自旋锁提供检查，这些检查与在早期 Windows 版本中提供给自旋锁的检查类似。 这些检查包括：

* 验证应该引发中断请求级别 (IRQL) 值（如 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))）的操作是否确实降低了 irql 值。

* 验证应降低 IRQL 值（如 [**KeReleaseInStackQueuedSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)）的操作是否实际上不会引发 irql 值。

* 如果启用了 [强制 Irql 检查](force-irql-checking.md) 选项，则在将 irql 提升为调度 \_ 级别或更高级别或更高版本时，如果在驱动程序以提升的 IRQL 运行时尝试公开可分页内存的可能引用，则修整系统进程的工作集。

* 在启用死锁检测选项时预测可能的死锁。

* 尝试在 \_ 启用死锁检测选项时，将相同的 KSPIN 锁数据结构同时用作旋转锁和堆栈排队自旋锁。

* 检查明显不正确的指针值，如用作旋转锁地址的用户模式虚拟地址。

* 正在驱动程序验证程序 IRQL 日志中记录 IRQL 转换。 当你使用 Windows 调试器的 **！ verifier 8** 扩展时，将显示此信息。 请参阅 [**！ verifier**](../debugger/-verifier.md)。

## <a name="additional-debugging-information"></a>其他调试信息

在 Windows 7 中，驱动程序验证程序提供了以下可用于调试的其他信息：

对于从已验证的驱动程序到 [**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) 和 [**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) 的最近调用，有一个按时间顺序排列的日志。 日志内容通过使用 Windows 调试器的 **！ verifier 0x200** 调试器扩展来显示。 此信息可用于了解某个线程在关键区域中意外运行或试图离开其现有关键区域的情况。

可以使用 **！ verifier 0x40** 调试器扩展显示 "[强制挂起 I/o 请求](force-pending-i-o-requests.md)" 日志中的其他信息。 在早期的 Windows 版本中，该日志只包含驱动程序验证程序被迫挂起的每个 IRP 的一个堆栈跟踪。 这是从第一次调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 的时间到强制挂起 IRP 的堆栈跟踪。 对于每个强制挂起的 IRP，Windows 7 至少有两个日志条目，可能多于两个：

* 当驱动程序验证器选取 IRP 强制挂起时，堆栈跟踪。 当某个已验证的驱动程序调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)时，驱动程序验证器选择某些要强制挂起的 irp。
* 完成后，强制挂起 IRP 的每个 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 调用的堆栈跟踪到达已验证的驱动程序。 同一 IRP 可以有多个 **IoCompleteRequest** 调用，因为其中一个驱动程序可以暂时停止完成例程的完成，然后再次调用 **IoCompleteRequest** 来恢复完成。

IRQL 转换日志中存在更有效的堆栈跟踪。 使用 **！ verifier 8** 显示此日志。 在 Windows 7 之前的 Windows 版本中，驱动程序验证程序可能已尝试在提升的 IRQL 上记录其中一些堆栈跟踪，因此无法捕获堆栈跟踪，因为存在高 IRQL 值。 在 Windows 7 中，驱动程序验证程序尝试捕获这些堆栈跟踪：

* 在引发 IRQL 之前（例如，在已验证的驱动程序调用 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)时）。
* 降低 IRQL 后，在已验证的驱动程序调用 [**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)时。

通过这种方式，驱动程序验证程序可以捕获更多的 IRQL 转换堆栈跟踪。

**！分析** 可以会审由增强的 i/o 验证程序检查公开的问题， (是 Windows 7 中的 i/o 验证程序) 的一部分。 在早期版本的 Windows 版本中，增强的 i/o 验证程序错误报告包括显示驱动程序验证程序检测到的驱动程序缺陷的说明，并将其中断到调试器。 运行 **！** 在此类中断后进行分析不会导致对其中许多中断有意义的会审，因为 **！分析** 不能使用调试器中显示的错误说明文本中的信息。 在 Windows 7 中，驱动程序验证器会将有关这些驱动程序缺陷的有意义信息保存在内存中。 **！分析** 可以找到此信息，并为许多这类中断执行更有意义的自动会审。

## <a name="driver-verifier-in-windows-vista-updated-february-9-2009"></a>Windows Vista 中的驱动程序验证程序 (*更新：2009年2月9日*) 

对于 Windows Vista，驱动程序验证程序已通过新的测试和功能得到了增强。

* 在不重新启动的情况下启用驱动程序验证程序和更改设置
* 增强的低资源模拟
* 强制挂起 I/O 请求
* 安全检查
* 更彻底的 i/o 验证
* 增强的 IRQL 检查
* 其他检查
* 锁定内存页跟踪
* 其他自动检查

## <a name="driver-verifier-in-windows-xp-updated-december-4-2001"></a>Windows XP 中的驱动程序验证程序 (*更新：2001年12月4日*) 

驱动程序验证程序是用于监视 Windows 内核模式驱动程序和图形驱动程序的工具。 Microsoft 强烈建议硬件制造商用驱动程序验证程序测试其驱动程序，以确保驱动程序不会进行非法的函数调用或导致系统损坏。 驱动程序验证程序已通过适用于 Microsoft Windows XP 的新测试和功能得到了增强。

提交给 WHQL 进行测试的驱动程序必须通过驱动程序验证器。 Windows XP 中的新驱动程序验证程序功能包括：

* 驱动程序验证器管理器是一个全新的图形用户界面， (GUI) 用于 verifier.exe
* 新的监视堆栈切换的自动检查
* 用于 DMA 验证的新的驱动程序验证程序选项 (也称为 HAL 验证) 、死锁检测和 SCSI 验证
* 结合了 "Level 1" 和 "Level 2" 测试的 i/o 验证更改，可选的增强型 i/o 验证测试
* 新调试器扩展 [**！死锁**](../debugger/-deadlock.md) 和 [**！ dma**](../debugger/-dma.md)
* 新 bug 检查： 0xE6 (驱动程序 \_ 验证程序 \_ DMA \_ 冲突) 和 0xF1 (SCSI \_ 验证程序 \_ 检测到 \_ 冲突) 
* 现有 bug 检查代码0xC4 和0xC9 的附加子代码

驱动程序验证程序功能还包括：

* **新的验证程序命令行选项** verifier.exe 实用程序有一个新参数 *VolatileDriverList*，它可与 **/adddriver** 关键字一起使用，以指定要添加到易失性设置的驱动程序列表。 *VolatileDriverList* 可以与 **/removedriver** 关键字一起使用，以指定要删除的驱动程序列表。
* **New！ verifier extension** New [**！**](../debugger/-verifier.md) 当监视资源不足或 IRQL 引发和旋转锁时，验证程序扩展显示额外的日志信息。 还提供联机帮助。
  * 使用0x4 设置的 *标志* 将导致显示包含驱动程序验证器在低资源模拟期间注入的错误日志
  * 使用0x8 设置的 *标志* 将导致显示包含所验证驱动程序所做的最新 IRQL 更改的日志
  * 如果 *Flags* 等于0x4 或0x8，则数量参数指定要包含在显示中的记录数或日志条目数
  * **?** 参数显示简短帮助文本

* 驱动程序验证程序管理器的联机帮助可通过以下方式之一显示驱动程序验证器管理器的联机帮助：
  * 选择并按住 (或右键) 单击 "驱动程序验证器管理器" 窗口中的某个项，然后从弹出菜单中选择 **"这是什么？"** 。
  * 在窗口右上角选择问号 (**？**) ，然后在 "驱动程序验证器管理器" 窗口中选择一个项。
