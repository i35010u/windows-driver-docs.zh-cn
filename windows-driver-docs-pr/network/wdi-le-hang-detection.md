---
title: LE 挂起检测
description: 本部分介绍 WDI 中的 LE 挂起检测
ms.assetid: 9C0BB4B8-184A-4C1A-8B47-C30C8318AEEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ba9c1869ed577ec7be205e152ed90726a86a703
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211541"
---
# <a name="le-hang-detection"></a>LE 挂起检测


某些固件具有可检测到固件挂起的监视器计时器。  (LE) 的一些 IHV 驱动程序具有逻辑来检测固件是否不会进行转发。 该 UE 允许 LE 指明此类条件。

指示应位于适配器端口 (例如，portid = 0xFFFF) 。 默认情况下，指示会触发 LE 执行完整的重置恢复过程，调用诊断，收集调试信息，并请求 PLDR。

当 LE 或固件监视程序计时器检测到固件停止时，UE 的期望如下所示。

1.  如果为 D0，
    1.  该 LE 指示 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 固件已 \_ 停止](./ndis-status-wdi-indication-firmware-stalled.md)。
    2.  在从指示返回时，LE 返回 (如果任何) 停止 WDI 命令。
    3.  UE) 过程开始重置恢复 (RR。

2.  如果在 Dx 中，这种情况只能在固件检测到延迟时进行。
    1.  固件引发唤醒中断。
    2.  收到 D0 命令后，指示固件停止的原因的唤醒原因。
    3.  返回 D0 WDI OID 后，LE 指示 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 固件 \_ 停止](./ndis-status-wdi-indication-firmware-stalled.md)。
    4.  以 D0：1a、1b 和1c 的形式完成该过程。

![wdi le 挂起检测](images/wdi-le-hang-detection-flow.png)

## <a name="hang-detection-in-dx"></a>Dx 中的挂起检测


此固件可能会在 Dx 停止进度。 在这种情况下，Dx D3Hot 用于 PCIe NIC，D2 适用于 USB 和 SDIO。 NIC 有权唤醒，并应自主维护访问点关联，或扫描 NLO （如果没有关联）。

如果 NIC 位于 Dx，则会阻止与主机的通信，因为总线可能处于关机状态。 因此，该 LE 无法检测到停止固件。 如果代码的唤醒部分仍处于活动状态，则固件本身必须检测条件并引发唤醒行 () 将堆栈通过 ACPI 或总线正在完成的方式间接引入 D0，NDIS 等待 \_ 唤醒 \_ irp。 因此，NDIS 会将 D0 设置为 NIC。

固件断言会唤醒此类条件。 该 LE 应指示固件延迟的唤醒原因。 唤醒原因 **WDI \_ 唤醒 \_ 原因 \_ 代码 \_ 固件 \_ 停止** 定义为具有其他唤醒原因的枚举。

若要在此方案中使用重置恢复，至少有两部分固件仍可正常工作。

1.  挂起检测代码。
2.  用于断言唤醒中断的代码。

如果没有任何一个，则主机端不知道固件是否已停止，并且不会发生 RR。 此方案不是设计目标的一部分。

![dx 中的 wdi 挂起检测](images/wdi-hang-detection-dx.png)

## <a name="os-module-triggered-reset-recovery"></a>OS 模块触发重置恢复


这是针对 Ihv 的信息。 除了检测到 UE 和 LE 挂起以外，其他 OS 组件还可能检测到挂起，并/或触发 UE 来调用重置恢复过程。 目前，Windows 10 中的 user mode wlansvc 组件在检测到与 Internet 连接的连接后，可能会请求将重置恢复到 UE，并在一段时间内失去对 DNS 服务器的访问权限。 将来，Microsoft 可能会发现触发重置恢复以增强最终用户体验的其他案例。

## <a name="related-topics"></a>相关主题


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 固件 \_ 停止](./ndis-status-wdi-indication-firmware-stalled.md)

[**WDI \_ TLV \_ 指示 \_ 唤醒 \_ 原因**](./wdi-tlv-indication-wake-reason.md)

 

