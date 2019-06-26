---
title: UE 挂起检测步骤 1 至 14 日
description: 步骤 1 到 14 的 UE 挂起检测如下所述。 步骤对应于 UE 挂起检测和恢复流中所示的图表。
ms.assetid: 0F6F9B31-27FB-44B1-8C0E-A270E8BAF295
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d342bcbe9ab7a11cf9f72aa9dcd9c894c3b327f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357102"
---
# <a name="ue-hang-detection-steps-1-14"></a>UE 挂起检测：步骤 1 至 14 日


步骤 1 到 14 的 UE 挂起检测如下所述。 步骤对应于关系图中所示[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)。

此示例使用 OID\_设置\_电源。

1.  NDIS 接收系统电源 IRP 或 NIC 当前引用降为 0。
2.  NDIS 生成 OID\_设置\_POWER D3 到 WDI 驱动程序。
3.  WDI WDI 命令 (M1) 包括一项任务，再发送下 LE WDI OID 将计时器设置为。 如果该命令是一项任务，也设置为任务的其他计时器。 这两个计时器可能会超时，但最多只有一个可触发重置恢复。
4.  WDI 将 WDI 命令发送到 LE。 LE 的推荐方法是记住 WDI OID 适配器结构中，如果它需要固件的命令以完成 OID。 当固件 WDI OID 的完成作业时，LE 完成 OID 并将其从适配器结构删除。 WDI 序列化到 LE Oid、 LE 必须只有一个槽记住挂起 WDI OID。 如果挂起固件命令、 LE 时可返回 OID 在任何时间，但不是晚于意外的删除 （它可以是意外删除的上下文中） 在步骤 17 中固件已被禁用。 对于任何其他情况，LE 只需完成 WDI OID 完成固件相应的作业，而不考虑它是否之前或之后诊断回调。 如果 LE 需要记住 WDI OID 诊断后，它需要记住它的另一个槽。 但是，对于诊断后接收到的 Oid，LE 应触摸以避免级联的挂起的固件。
5.  LE 将命令发送到固件。
6.  如果固件命令超时，它可能是由于固件挂起或太长。
    -   如果固件只需时间太长，若要在超时时间后完成该命令，LE 可以完成 WDI 命令。 UE 适当地处理它。
    -   如果固件已经被挂起，则不会很快完成 WDI 命令。 LE 时必须完成它在意外删除在步骤 16 硬件已被重置，以便安全地完成而无需特殊处理的潜在的争用条件。

7.  WDI 计时器将激发生成 WDI 诊断命令。 此 WDI 命令是 LE 驱动程序，在调用[ *MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)，而不是 WDI OID。
8.  LE 收集硬件控件注册状态，以及 （可选） 的完整的固件状态。
    -   IHV 驱动程序应收集硬件寄存器的内容，它被限制为 1 KB，并将其返回函数返回结果中。 此外，在预生产环境中，LE 应还尝试固件上下文转储到文件，这样，IHV 可以全面执行事后调试。 开关可作为一个注册表项来控制硬件寄存器和固件映像的集合。
    -   LE 还将标记为取消当前的命令。 如果命令完成争用极具竞争力诊断，则可接受如果 LE 不为此命令执行任何操作。
    -   使用此命令挂起，UE 可能会发送进一步的 WDI 命令作为重置操作的结果。 这些是正在进行的命令或清理命令。 在诊断调用后，LE 应处理它们无需接触固件。

9.  WDI 接收控件注册状态。
10. WDI 标记挂起 WDI 命令，以便通过 LE 指示更高版本。
11. WDI 返回 （完成） 而未 WDI 完成 NDIS 命令。 这是安全因为 WDI 双缓冲区 NDIS 命令。
12. WDI 调用 NDIS 重置并调用[ **NdisWriteErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiswriteerrorlogentry)与*错误代码*的**NDIS\_错误\_代码\_硬件\_失败**(0xc000138a)。 这会导致在 LE 的模块名称在系统事件日志中记录的事件。 错误事件 ID 自动弹出作为 (0xc000138a | 0xffff) – 0n5002。 LE 也使用相同的错误代码来写入错误日志，如果数据的第一个 dword 值应包含高位集 (0x80000000) 轻松地单独的事件按 LE。 WDI 使用 0x00000000 到 0x7fffffff 的第一个 DWORD 数据。
13. 调用返回。
14. NDIS 完成 IRP。

此点之后，NDIS 调用总线意外删除和重新枚举我们。 请务必注意 WDI 双缓冲区 NDIS 命令，以便它不需要等待 WDI 命令返回完成 NDIS 命令。 这消除了 LE 执行取消逻辑，是非常复杂，无法执行操作的需求。

完成的 NDIS OID\_设置\_POWER 是为了避免死锁的即插即用操作。 所有 PnP 和电源状态更改事件进行序列化。 这意味着，如果集 power OID 不返回，NDIS 不能返回集 power IRP，这意味着与意外删除 IRP 重置恢复锁定。

## <a name="related-topics"></a>相关主题


[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)

[重置 （意外删除）： 步骤 15 到 20](wdi-reset--surprise-remove---steps-15-20.md)

[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)

 

 






