---
title: UE 挂起检测步骤1-14
description: 下面介绍了 UE 挂检测的步骤1到14。 这些步骤对应于 UE 挂起检测和恢复流中显示的关系图。
ms.assetid: 0F6F9B31-27FB-44B1-8C0E-A270E8BAF295
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63524cfacbb0f651a5ac56cccf7727ab5bfe22d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841709"
---
# <a name="ue-hang-detection-steps-1-14"></a>UE 挂起检测：步骤1-14


下面介绍了 UE 挂检测的步骤1到14。 这些步骤对应于[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)中显示的关系图。

此示例使用\_设置\_功能的 OID。

1.  NDIS 接收系统电源 IRP，或 NIC 活动引用降到0。
2.  NDIS\_将\_POWER D3 设置为 WDI 驱动程序。
3.  WDI 为 WDI 命令（M1）设置计时器，并在将 WDI OID 发送到 LE 之前包含任务。 如果命令为任务，则还会设置任务的其他计时器。 这两个计时器可能会超时，但最多只能有一个触发重置恢复。
4.  WDI 将 WDI 命令发送到 LE。 如果需要提供固件命令来完成 OID，则该 LE 的建议是在适配器结构中记住 WDI OID。 当固件完成 WDI OID 的作业时，LE 将完成 OID，并从适配器结构中删除它。 由于 WDI 将 Oid 序列化到 LE，因此 LE 只需要一个槽来记住挂起的 WDI OID。 如果固件命令挂起，则在禁用固件后，LE 可随时返回 OID，但在步骤17时，它可能会在出现意外删除的情况下返回 OID。 对于任何其他情况，该 LE 在固件完成相应的作业时只完成 WDI OID，而不考虑它是在诊断回调之前还是之后。 如果该 LE 需要在诊断后记住 WDI OID，则需要另一个槽来记住它。 但是，对于诊断后收到的 Oid，该 LE 不应触及固件以避免级联挂起。
5.  LE 向固件发送命令。
6.  如果固件命令超时，则可能是由于固件挂起或时间太长。
    -   如果固件完成后，只需很长时间才能完成该命令，则 LE 可以完成 WDI 命令。 UE 会适当地处理。
    -   如果固件挂起，WDI 命令将不会立即完成。 如果重置硬件，则必须在步骤16中将其意外完成，因此，该 LE 必须完全删除，这样就可以安全地完成，而无需特殊处理潜在的争用情况。

7.  触发 WDI 计时器以生成 WDI 的诊断命令。 此 WDI 命令将调用 LE 驱动程序[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)，而不是 WDI OID。
8.  LE 收集硬件控制寄存器状态，还可以选择完全固件状态。
    -   IHV 驱动程序应收集限制为1KB 的硬件寄存器内容，并将其返回到函数返回中。 此外，在预生产环境中，该 LE 还应尝试将固件上下文转储到文件中，以便 IHV 可以彻底执行事后调试。 交换机可以作为注册表项实现，以控制硬件寄存器和固件映像的集合。
    -   该 LE 还将当前命令标记为取消。 如果命令完成争用诊断，则如果该命令不执行任何操作，则可以接受。
    -   完成此命令后，UE 可能会发送更多 WDI 命令，作为重置的后果。 这些是正在进行的命令或清理命令。 诊断调用之后，该 LE 应处理它们，而不会接触固件。

9.  WDI 接收控制寄存器状态。
10. WDI 标记挂起 WDI 命令，以使其在该 LE 之后指示。
11. WDI 返回（完成） NDIS 命令，但没有 WDI 完成。 这是安全的，因为 WDI 会对 NDIS 命令进行双缓冲。
12. WDI 调用 NDIS 来重置并调用[**NdisWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteerrorlogentry) ，*错误代码*为**ndis\_错误\_代码\_硬件\_故障**（0xc000138a）。 这将导致事件记录在系统事件日志中，模块名称为 LE。 错误事件 ID 会自动弹出，如（0xc000138a | 0xffff）-0n5002。 如果该 LE 还使用相同的错误代码来写入错误日志，则数据的第一个 DWORD 应包含高位集（0x80000000），以方便地通过 LE 分隔事件。 WDI 使用0x00000000 来实现第一个 DWORD 数据。
13. 调用返回。
14. NDIS 完成 IRP。

在此之后，NDIS 会调用总线来意外删除并重新枚举我们。 务必要注意的是，WDI 双缓冲 NDIS 命令，使其不必等待 WDI 命令返回完成 NDIS 命令。 这样，便无需执行 "取消逻辑" 这一操作。

完成 NDIS OID\_设置\_功能是为了避免 PnP 操作的死锁。 序列化所有 PnP 和电源状态变化事件。 这意味着，如果已设置的电源 OID 未返回，NDIS 将无法返回 Set power IRP，这意味着重置恢复会锁定并返回 "意外删除" IRP。

## <a name="related-topics"></a>相关主题


[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)

[Reset （意外删除）：步骤15-20](wdi-reset--surprise-remove---steps-15-20.md)

[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)

 

 






