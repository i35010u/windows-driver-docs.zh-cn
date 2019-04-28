---
title: 驱动程序验证程序选项
description: Driver Verifier 选项和规则类
ms.assetid: f251fe07-e68e-4d93-9aa5-9a0bc818756d
keywords:
- 驱动程序验证程序 WDK，列出的选项
- 错误 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 829f01e45313f91d82fbf6dda7ff4c593f7e304e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344837"
---
# <a name="driver-verifier-options-and-rule-classes"></a>Driver Verifier 选项和规则类


本主题介绍的可选功能和驱动程序验证程序中的规则类。 请参阅[标准设置](#standard-settings)有关时使用的标准设置，包括的选项的列表。

> [!NOTE]
> 某些[自动检查](automatic-checks.md)始终执行上的驱动程序，正在验证，而不考虑该选择选项。 如果该驱动程序不正确的 IRQL 在使用内存、 未正确调用或释放自旋锁和内存分配、 不正确切换堆栈，或释放内存池，而无需首先删除计时器，驱动程序验证程序将检测此行为。 卸载该驱动程序时，驱动程序验证程序将检查以查看其已正确发布其资源。

## <a name="enabling-rule-classes-with-ruleclasses"></a>启用具有 /ruleclasses 规则类

从 Windows 10，版本 17627 及更高版本，可以启用规则类具有以下语法：

`/ruleclasses or /rc [<ruleclass_1> <ruleclass_2> ... <ruleclass_k>]`

请注意，启用多个类 （表示正下方的十进制整数） 时，请用空格字符分隔每个整数。 

可在下面找到这些规则类的说明。

### <a name="standard-rule-classes"></a>标准规则类

| 规则类 | 十进制 ID |
| -- | -- |
| 特殊的池        | 1 |
| 强制 IRQL 检查 | 2 |
| 池跟踪       | 4 |
| I/O 验证    | 5 |
| 死锁检测  | 6 |
| DMA 检查 | 8 |
| 安全检查 | 9 |
| 其他检查 | 12 |
| DDI 合规性检查 | 18 |
| WDF 验证 | 34 |

### <a name="additional-rule-classes"></a>其他规则类

这些规则类专用于特定方案测试。 规则类标有 (\*) 要求将自动启用的 I/O 验证 (5)。 标志标记有 (\**) 支持禁用的单个规则。

| 规则类 | 十进制 ID |
| -- | -- |
| 随机的资源不足模拟        | 3 |
| 强制挂起 I/O 请求 （*） | 10 |
| IRP 日志记录       | 11 |
| 固定 MDL 堆栈 （*） 检查    | 14 |
| 固定 MDL 驱动程序 （*） 的检查  | 15 |
| 电源框架延迟模糊 | 16 |
| 端口/微型端口接口检查 | 17 |
| 系统性资源不足模拟 | 19 |
| DDI 符合性检查 （其他） | 20 |
| 内核同步延迟模糊处理 | 24 |
| VM 交换机验证 | 25 |
| 代码完整性检查 | 22 |

## <a name="optional-feature-and-rule-class-descriptions"></a>可选的功能和规则类描述 

[特殊的池](special-pool.md)
    
启用此选项后，驱动程序验证程序会将分配驱动程序的内存请求的最特殊的池。 将会监控此特殊池是否存在内存溢出、内存欠载和内存在释放后仍可访问的情况。

[强制 IRQL 检查](force-irql-checking.md)

启用此选项后，驱动程序验证程序将极限内存压力置于驱动程序通过使可分页代码无效。 如果驱动程序尝试访问错误 IRQL 处的分页内存或持有旋转锁，则驱动程序验证程序将会检测到此行为。

[低资源模拟](low-resources-simulation.md)(称为*随机化的资源不足模拟*在 Windows 8.1)

启用此选项后，驱动程序验证程序将随机失败池分配请求和其他资源请求。 通过将这些分配故障注入到系统中，驱动程序验证程序可以测试驱动程序处理资源不足情况的能力。

[跟踪的池](pool-tracking.md)

启用此选项后，驱动程序验证程序检查驱动程序卸载时是否已释放其所有内存分配。 这将发现内存泄漏。

[I/O 验证](i-o-verification.md)

时此选项处于活动状态，驱动程序验证程序会将驱动程序的 Irp 分配一个特殊的池，并监视驱动程序的 I/O 处理。 这将检测 I/O 例程的使用是否非法或不一致。

[死锁检测](deadlock-detection.md)

(Windows XP 及更高版本)如果此选项处于活动状态，驱动程序验证程序将监视的自旋锁、 互斥体和快速的互斥体的驱动程序的使用。 此选项可检测驱动程序的代码是否会导致有些时候死锁的可能性。

[增强的 I/O 验证](enhanced-i-o-verification.md)

(Windows XP 及更高版本)时此选项处于活动状态，驱动程序验证工具监视多个 I/O 管理器例程的调用并执行压力测试的 PnP Irp、 power Irp 和 WMI Irp。 在 Windows 7 和更高版本的 Windows 操作系统，增强的 I/O 验证的所有功能都都作为的一部分[I/O 验证](i-o-verification.md)和就不再可用，也不需要选择此选项在驱动程序验证程序管理器或从命令行。

[DMA 验证](dma-verification.md)

(Windows XP 及更高版本)如果此选项处于活动状态，驱动程序验证程序将监视 DMA 例程的驱动程序的使用。 这将检测 DMA 缓冲器、适配器和映射寄存器的使用是否不正确。

[安全检查](security-checks.md)

(Windows Vista 及更高版本)当此选项处于活动状态时，驱动程序验证程序查找可能会导致安全漏洞，如对用户模式地址由内核模式例程的引用的常见错误。

[杂项检查](miscellaneous-checks.md)

(Windows Vista 及更高版本)当此选项处于活动状态时，驱动程序验证程序将查找驱动程序故障，如释放的内存的处理不当的常见原因。

[强制挂起 I/O 请求](force-pending-i-o-requests.md)

(Windows Vista 及更高版本)驱动程序验证程序时此选项处于活动状态，测试驱动程序的响应状态\_PENDING 返回值通过返回状态\_随机调用 PENDING [ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336).

[IRP 日志记录](irp-logging.md)

(Windows Server 2003 及更高版本)时此选项处于活动状态，驱动程序验证程序将监视的 Irp 的驱动程序的使用，并创建的 IRP 使用的日志。

[磁盘完整性检查](disk-integrity-checking.md)

（Windows Server 2003 中引入。 不提供在 Windows 7 及更高版本。）当此选项处于活动状态时，驱动程序验证程序监视硬盘访问，并检测磁盘是否已正确地保留其数据。

[SCSI 验证](scsi-verification.md)

(Windows XP 及更高版本)当此选项处于活动状态时，驱动程序验证程序监视导出 SCSI 端口例程，过多延迟的使用不当的 SCSI 微型端口驱动程序，并 SCSI 的不正确处理请求。

[Storport 验证](dv-storport-verification.md)

(Windows Vista 及更高版本)如果此选项处于活动状态，驱动程序验证程序将监视导出的 Storport 例程、 过多延迟和 Storport 请求处理不当使用不当的 Storport 微型端口驱动程序。

[电源框架延迟模糊](concurrency-stress-test.md)

（从 Windows 8 开始）驱动程序验证程序时此选项处于活动状态，随机排列线程计划，以帮助刷新中使用的驱动程序的并发错误[电源管理框架 (PoFx)](https://msdn.microsoft.com/library/windows/hardware/hh406637)。 此选项不建议用于不直接利用电源管理框架 (PoFx) 的驱动程序...

[DDI 符合性检查](ddi-compliance-checking.md)

（从 Windows 8 开始）时此选项处于活动状态，驱动程序验证程序应用一组检查驱动程序和操作系统的内核接口之间的正确交互的设备驱动程序接口 (DDI) 规则。

[面向堆栈的固定 MDL 检查](invariant-mdl-checking-for-stack.md)

（从 Windows 8 开始）[MDL 堆栈检查固定](invariant-mdl-checking-for-stack.md)选项监视驱动程序如何跨驱动程序堆栈处理固定 MDL 缓冲区。 驱动程序验证程序可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，必须在至少一个驱动程序上启用 I/O 验证。

[面向驱动程序的固定 MDL 检查](invariant-mdl-checking-for-driver.md)

（从 Windows 8 开始）[驱动程序检查固定 MDL](invariant-mdl-checking-for-driver.md)选项监视驱动程序如何处理在每个驱动程序的基础上的固定 MDL 缓冲区。 此选项可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，你必须在至少一个驱动程序上启用 I/O 验证。

[基于堆栈的故障注入](stack-based-failure-injection.md)

（仅适用于 Windows 8 和 WDK 8）[基于堆栈的故障注入](stack-based-failure-injection.md)选项注入资源故障。 内核模式驱动程序中的。 此选项结合使用了特殊驱动程序 KmAutoFail.sys 和[驱动程序验证程序](driver-verifier.md)来侵入驱动程序错误处理路径。

[系统资源不足模拟](systematic-low-resource-simulation.md)

（从 Windows 8.1 开始）[系统资源不足模拟](systematic-low-resource-simulation.md)选项注入资源故障。 内核模式驱动程序中的。

[NDIS/WIFI 验证](ndis-wifi-verification.md)

（从 Windows 8.1 开始）时此选项处于活动状态，驱动程序验证程序适用 NDIS 和检查之间的 NDIS 微型端口驱动程序和操作系统内核正确交互的无线 LAN (WIFI) 规则的集。

[内核同步延迟模糊](kernel-synchronization-delay-fuzzing.md)

（从 Windows 8.1 开始）此选项随机排列线程计划，以帮助检测驱动程序中的并发 bug。

[VM 交换机验证](vm-switch-verification.md)

（从 Windows 8.1 开始）此选项可监视筛选器驱动程序 (*可扩展交换机扩展*) 内运行[HYPER-V 可扩展交换机](https://msdn.microsoft.com/library/windows/hardware/hh598161)。

[检查端口/微型端口接口](port-miniport-interface-checking.md)

检查端口/微型端口接口使驱动程序验证程序检查 PortCls.sys 和其音频微型端口驱动程序，以及 ks.sys 和其 AVStream 微型端口驱动程序之间的 DDI 接口。 请参阅有关 AVStream 驱动程序的规则和规则的音频驱动程序。

[代码完整性检查](code-integrity-checking.md)

当使用基于虚拟化的安全隔离代码完整性，内核内存可能会变得可执行文件的唯一方法是通过代码完整性验证。 这意味着可写内容和可执行文件 (W + X) 的内核内存页面可以永远不会是不能直接修改可执行代码。 代码完整性检查确保这样的代码完整性规则，兼容性，并检测冲突。

[WDF 验证](wdf-verification.md)

WDF 验证检查的内核模式驱动程序是否是正确遵循内核模式驱动程序框架 (KMDF) 要求。 


## <a name="standard-settings"></a>标准设置

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">包含在标准设置中的选项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊的池</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">强制 IRQL 检查</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">跟踪的池</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O 验证</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">发生死锁检测</a>(Windows XP 及更高版本)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">增强的 I/O 验证</a>（在 Windows 7 及更高版本，此选项将自动激活时选择的 I/O 验证）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA 验证</a>(Windows XP 及更高版本)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">安全检查</a>(Windows XP 及更高版本)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">杂项检查</a>(Windows Vista 及更高版本)</p></td>
</tr>
<tr class="even">
<td align="left"><a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 符合性检查</a>（从 Windows 8 开始）</td>
</tr>
</tbody>
</table>

 

## <a name="driver-verifier-options-that-require-io-verification"></a>Driver Verifier 选项需要 I/O 验证


有四个选项需要你先启用 [I/O 验证](i-o-verification.md)。 如果未启用 I/O 验证，则无法启用这些选项。

-   [强制挂起 I/O 请求](force-pending-i-o-requests.md)
-   [IRP 日志记录](irp-logging.md)
-   [面向堆栈的固定 MDL 检查](invariant-mdl-checking-for-stack.md)
-   [面向驱动程序的固定 MDL 检查](invariant-mdl-checking-for-driver.md)

 

 





