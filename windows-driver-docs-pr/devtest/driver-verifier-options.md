---
title: 驱动程序验证程序选项
description: 驱动程序验证程序选项和规则类
ms.assetid: f251fe07-e68e-4d93-9aa5-9a0bc818756d
keywords:
- 驱动程序验证程序 WDK，列出的选项
- 错误 WDK 驱动程序验证程序
ms.date: 04/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: 95f9bec69d0bfa4d54f1dadce31c5db2cfb55b38
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/11/2020
ms.locfileid: "81208134"
---
# <a name="driver-verifier-options-and-rule-classes"></a>驱动程序验证程序选项和规则类


本主题介绍了驱动程序验证器中的可选功能和规则类。 使用标准设置时，请参阅[标准设置](#standard-settings)以了解所包含的选项列表。

> [!NOTE]
> 某些[自动检查](automatic-checks.md)始终在正在验证的驱动程序上执行，而不考虑已选择的选项。 如果驱动程序使用不正确的 IRQL 的内存，则不正确地调用或释放旋转锁和内存分配，不正确地切换堆栈，或者释放内存池而不先删除计时器，驱动程序验证程序将检测到此行为。 卸载驱动程序时，驱动程序验证器将检查其是否已正确释放其资源。

## <a name="enabling-rule-classes-with-ruleclasses"></a>通过/ruleclasses 启用规则类

从 Windows 10 版本17627及更高版本开始，可以使用以下语法启用规则类：

`/ruleclasses or /rc [<ruleclass_1> <ruleclass_2> ... <ruleclass_k>]`

请注意，启用多个类（用下面的十进制整数表示）时，请用空格字符分隔每个整数。 

可在下面找到这些规则类的说明。

### <a name="standard-rule-classes"></a>标准规则类

| 规则类 | 小数 ID |
| -- | -- |
| 特殊池        | 1 |
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

这些规则类用于特定的方案测试。 规则类标记为（\*）需要自动启用的 i/o 验证（5）。 标记为（\**）的标志支持禁用单个规则。

| 规则类 | 小数 ID |
| -- | -- |
| 随机低资源模拟        | 3 |
| 强制挂起 i/o 请求（*） | 10 |
| IRP 日志记录       | 11 |
| 堆栈的固定 MDL 检查（*）    | 14 |
| 驱动程序的固定 MDL 检查（*）  | 15 |
| Power framework 延迟模糊 | 16 |
| 端口/微型端口接口检查 | 17 |
| 系统性资源不足模拟 | 19 |
| DDI 相容性检查（其他） | 20 |
| 内核同步延迟模糊处理 | 24 |
| VM 交换机验证 | 25 |
| 代码完整性检查 | 26 |
| 其他 IRQL 检查 | 35 |

## <a name="optional-feature-and-rule-class-descriptions"></a>可选功能和规则类说明

[特殊池](special-pool.md)

如果启用此选项，则驱动程序验证器将从特殊池分配大部分驱动程序的内存请求。 将会监控此特殊池是否存在内存溢出、内存欠载和内存在释放后仍可访问的情况。

[强制执行 IRQL 检查](force-irql-checking.md)

如果启用此选项，则驱动程序验证器会通过使可分页代码无效来对驱动程序施加极大的内存压力。 如果驱动程序尝试访问错误 IRQL 处的分页内存或持有旋转锁，则驱动程序验证程序将会检测到此行为。

[低资源模拟](low-resources-simulation.md)（在 Windows 8.1 中称为*随机低资源模拟*）

当启用此选项时，驱动程序验证程序会随机失败池分配请求和其他资源请求。 通过将这些分配故障注入到系统中，驱动程序验证程序可以测试驱动程序处理资源不足情况的能力。

[池跟踪](pool-tracking.md)

如果启用此选项，则驱动程序验证程序将检查驱动程序验证程序是否在卸载时释放了其所有的内存分配。 这会揭示内存泄漏。

[I/o 验证](i-o-verification.md)

当此选项处于活动状态时，驱动程序验证器将从特殊池分配驱动程序的 Irp，并监视驱动程序的 i/o 处理。 这将检测 I/O 例程的使用是否非法或不一致。

[死锁检测](deadlock-detection.md)

（Windows XP 及更高版本）此选项处于活动状态时，驱动程序验证器会监视驱动程序对自旋锁、互斥体和快速互斥体的使用情况。 这会检测驱动程序的代码是否有可能在某一时刻导致死锁。

[增强的 i/o 验证](enhanced-i-o-verification.md)

（Windows XP 及更高版本）此选项处于活动状态时，Driver Verifier 会监视多个 i/o 管理器例程的调用，并对 PnP Irp、电源 Irp 和 WMI Irp 执行压力测试。 在 windows 7 和更高版本的 Windows 操作系统中，增强的 i/o 验证的所有功能都包含在[I/o 验证](i-o-verification.md)的一部分中，它不再可用，也无法在驱动程序验证器管理器或命令行中选择此选项。

[DMA 验证](dma-verification.md)

（Windows XP 及更高版本）此选项处于活动状态时，Driver Verifier 会监视驱动程序对 DMA 例程的使用情况。 这将检测 DMA 缓冲器、适配器和映射寄存器的使用是否不正确。

[安全检查](security-checks.md)

（Windows Vista 和更高版本）此选项处于活动状态时，驱动程序验证器会查找可能导致安全漏洞的常见错误，如内核模式例程对用户模式地址的引用。

[其他检查](miscellaneous-checks.md)

（Windows Vista 和更高版本）此选项处于活动状态时，驱动程序验证器将查找驱动程序崩溃的常见原因，如 mishandling 的内存。

[强制挂起 I/O 请求](force-pending-i-o-requests.md)

（Windows Vista 和更高版本）当此选项处于活动状态时，驱动程序验证器通过将随机调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的状态返回\_，来测试驱动程序对状态\_等待返回值的响应。

[IRP 日志记录](irp-logging.md)

（Windows Server 2003 及更高版本）此选项处于活动状态时，Driver Verifier 会监视驱动程序使用的 Irp，并创建 IRP 使用的日志。

[磁盘完整性检查](disk-integrity-checking.md)

（在 Windows Server 2003 中引入。 在 Windows 7 和更高版本中不可用。）此选项处于活动状态时，Driver Verifier 会监视硬盘访问，并检测磁盘是否正在正确保留其数据。

[SCSI 验证](scsi-verification.md)

（Windows XP 及更高版本）此选项处于活动状态时，驱动程序验证器会监视 SCSI 微型端口驱动程序，以在不正确使用导出的 SCSI 端口例程、延迟过多以及不正确地处理 SCSI 请求。

[Storport 验证](dv-storport-verification.md)

（Windows Vista 和更高版本）此选项处于活动状态时，驱动程序验证器会监视 Storport 微型端口驱动程序，以在不正确使用导出的 Storport 例程、延迟过多以及不正确处理 Storport 请求。

[Power Framework 延迟模糊](concurrency-stress-test.md)

（从 Windows 8 开始）此选项处于活动状态时，驱动程序验证器随机化线程计划以帮助在使用[电源管理框架（PoFx）](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)的驱动程序中清理并发错误。 对于不直接利用电源管理框架（PoFx）的驱动程序，不建议使用此选项。

[DDI 相容性检查](ddi-compliance-checking.md)

（从 Windows 8 开始）此选项处于活动状态时，驱动程序验证器会应用一组设备驱动程序接口（DDI）规则，这些规则检查操作系统的驱动程序和内核接口之间的正确交互。

[面向堆栈的固定 MDL 检查](invariant-mdl-checking-for-stack.md)

（从 Windows 8 开始）"[固定 Mdl 检查堆栈](invariant-mdl-checking-for-stack.md)" 选项监视驱动程序如何处理驱动程序堆栈间的固定 mdl 缓冲区。 驱动程序验证程序可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，必须在至少一个驱动程序上启用 I/O 验证。

[面向驱动程序的固定 MDL 检查](invariant-mdl-checking-for-driver.md)

（从 Windows 8 开始）"[对驱动程序进行固定 Mdl 检查](invariant-mdl-checking-for-driver.md)" 选项监视驱动程序如何处理基于每个驱动程序的固定 mdl 缓冲区。 此选项可检测是否对固定 MDL 缓冲区进行了非法修改。 若要使用此选项，你必须在至少一个驱动程序上启用 I/O 验证。

[基于堆栈的故障注入](stack-based-failure-injection.md)

（仅适用于 Windows 8 和 WDK 8）[基于堆栈的故障注入](stack-based-failure-injection.md)选项注入内核模式驱动程序中的资源故障。 此选项结合使用了特殊驱动程序 KmAutoFail.sys 和[驱动程序验证程序](driver-verifier.md)来侵入驱动程序错误处理路径。

[系统低资源模拟](systematic-low-resource-simulation.md)

（从 Windows 8.1 开始）[系统低资源模拟](systematic-low-resource-simulation.md)选项注入内核模式驱动程序中的资源故障。

[NDIS/WIFI 验证](ndis-wifi-verification.md)

（从 Windows 8.1 开始）此选项处于活动状态时，驱动程序验证器会应用一组 NDIS 和无线 LAN （WIFI）规则，这些规则检查 NDIS 微型端口驱动程序和操作系统内核之间的正确交互。

[内核同步延迟模糊处理](kernel-synchronization-delay-fuzzing.md)

（从 Windows 8.1 开始）此选项随机化线程计划，以帮助检测驱动程序中的并发 bug。

[VM 交换机验证](vm-switch-verification.md)

（从 Windows 8.1 开始）此选项监视在[Hyper-v 可扩展交换机](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch)内运行的筛选器驱动程序（*可扩展交换机扩展*）。

[端口/微型端口接口检查](port-miniport-interface-checking.md)

端口/微型端口接口检查使驱动程序验证程序能够检查 PortCls 与其音频微型端口驱动程序之间的 DDI 接口，以及 ks 及其 AVStream 的微型端口驱动程序。 请参阅 AVStream 驱动程序的规则和音频驱动程序的规则。

[代码完整性检查](code-integrity-checking.md)

使用基于虚拟化的安全性来隔离代码完整性时，内核内存可执行的唯一方式是通过代码完整性验证。 这意味着内核内存页永远不能为可写且可执行（W + X）和可执行代码不能直接修改。 代码完整性检查确保这些代码完整性规则的兼容性并检测冲突。

[WDF 验证](wdf-verification.md)

WDF 验证检查内核模式驱动程序是否已正确遵循内核模式驱动程序框架（KMDF）要求。

[其他 IRQL 检查]()

其他 IRQL 检查增加了对 PASSIVE_LEVEL 的 DDI 相容性检查 IRQL 规则。 它包含以下两个规则：
- [IrqlIoRtlZwPassive](wdm-irqliortlzwpassive.md)规则指定，仅当该驱动程序以 IRQL = PASSIVE_LEVEL 执行时，才调用该规则中列出的 DDIs。
- [IrqlNtifsApcPassive](wdm-irqlntifsapcpassive.md)规则指定，仅当该驱动程序以 irql = PASSIVE_LEVEL 或以 irql < = APC_LEVEL 执行时，才调用该规则中列出的 DDIs。

## <a name="standard-settings"></a>标准设置

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标准设置中包含的选项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="force-irql-checking.md" data-raw-source="[Force IRQL Checking](force-irql-checking.md)">强制执行 IRQL 检查</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="pool-tracking.md" data-raw-source="[Pool Tracking](pool-tracking.md)">池跟踪</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/o 验证</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="deadlock-detection.md" data-raw-source="[Deadlock Detection](deadlock-detection.md)">死锁检测</a>（Windows XP 及更高版本）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">增强的 I/o 验证</a>（在 Windows 7 及更高版本中，当你选择 "i/o 验证" 时，此选项会自动激活）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="dma-verification.md" data-raw-source="[DMA Verification](dma-verification.md)">DMA 验证</a>（Windows XP 及更高版本）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="security-checks.md" data-raw-source="[Security Checks](security-checks.md)">安全检查</a>（Windows XP 及更高版本）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="miscellaneous-checks.md" data-raw-source="[Miscellaneous Checks](miscellaneous-checks.md)">杂项检查</a>（Windows Vista 和更高版本）</p></td>
</tr>
<tr class="even">
<td align="left"><a href="ddi-compliance-checking.md" data-raw-source="[DDI compliance checking](ddi-compliance-checking.md)">DDI 相容性检查</a>（从 Windows 8 开始）</td>
</tr>
</tbody>
</table>

## <a name="driver-verifier-options-that-require-io-verification"></a>需要 i/o 验证的驱动程序验证程序选项

有四个选项需要你先启用 [I/O 验证](i-o-verification.md)。 如果未启用 I/O 验证，则无法启用这些选项。

-   [强制挂起 I/O 请求](force-pending-i-o-requests.md)
-   [IRP 日志记录](irp-logging.md)
-   [面向堆栈的固定 MDL 检查](invariant-mdl-checking-for-stack.md)
-   [面向驱动程序的固定 MDL 检查](invariant-mdl-checking-for-driver.md)
