---
title: LE 挂起检测
description: 本部分介绍在 WDI LE 挂起检测
ms.assetid: 9C0BB4B8-184A-4C1A-8B47-C30C8318AEEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 966b6d52548c937c3479bab0af8736e855ad6950
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385481"
---
# <a name="le-hang-detection"></a>LE 挂起检测


某些固件具有可以检测到固件挂起监视计时器。 一些 IHV 驱动程序 (LE) 具有逻辑来检测固件都没有建立向前推进。 UE 允许 LE 以指示这种情况。

指示应在适配器端口上 (例如，portid = 0xFFFF)。 指示默认情况下触发 LE 若要执行完全重置恢复过程-调用诊断、 收集调试信息，并请求 PLDR。

LE 或固件监视计时器检测到固件停止时，从 UE 期望很，如下所示。

1.  如果在 D0，
    1.  指示 LE [NDIS\_状态\_WDI\_指示\_固件\_STALLED](https://msdn.microsoft.com/library/windows/hardware/dn925634)。
    2.  在从指示返回时，LE 返回 （如果有） 已停止的 WDI 命令。
    3.  UE 启动重置恢复 (RR) 过程。

2.  如果在 Dx，才会发生此与检测到的固件停滞。
    1.  固件引发唤醒中断。
    2.  在接收到 D0 命令，指示唤醒原因的固件停止的原因。
    3.  返回 D0 WDI OID 后, LE 指示[NDIS\_状态\_WDI\_指示\_固件\_STALLED](https://msdn.microsoft.com/library/windows/hardware/dn925634)。
    4.  完成 D0 中的过程：1a、 1b 和 1c。

![wdi le 挂起检测](images/wdi-le-hang-detection-flow.png)

## <a name="hang-detection-in-dx"></a>挂起检测 Dx 中


很可能固件停止 Dx 中的进度。 在这种情况下，Dx 是 D3Hot PCIe nic 和 USB 和 SDIO D2。 NIC 的知识来唤醒和预期自主，维护访问点关联，也可以扫描 NLO 如果未关联。

Dx NIC 时，由于总线可能是在关闭状态被阻塞到该主机通信。 因此，LE 不能够检测到已停止的固件。 固件本身已检测的条件并引发唤醒行 （如果唤醒一部分代码是仍保持活动状态） 将堆栈到 D0 间接通过 ACPI 或总线完成、 NDIS 等待\_唤醒\_irp。 因此，NDIS D0 设置到 nic。

固件断言唤醒为此类情况。 LE 应指示固件停滞唤醒原因。 唤醒原因**WDI\_唤醒\_原因\_代码\_固件\_STALLED**定义为与其他唤醒原因枚举。

对于重置恢复，以便在此方案中，至少两个部分的固件必须仍正常工作。

1.  挂起检测代码。
2.  要断言唤醒中断的代码。

如果缺乏两者中任何一个，在主机端不知道如果固件将停止，RR，不会发生。 这种情况下不是设计目标的一部分。

![在 dx wdi 挂起检测](images/wdi-hang-detection-dx.png)

## <a name="os-module-triggered-reset-recovery"></a>OS 模块触发重置恢复


这是信息性 ihv。 除了 UE 和 LE 检测到挂起，其他操作系统组件可能检测到挂起和/或触发 UE 调用重置恢复过程。 目前，Windows 10 中的用户模式 wlansvc 组件可能会请求重置恢复到 UE 时它检测 Internet 连接的连接并随后将失去访问而无需一段时间的解除关联的 DNS 服务器的能力。 将来，Microsoft 可能会发现其他用例附加到触发器重置的恢复，以增强最终用户体验。

## <a name="related-topics"></a>相关主题


[NDIS\_状态\_WDI\_指示\_固件\_STALLED](https://msdn.microsoft.com/library/windows/hardware/dn925634)

[**WDI\_TLV\_INDICATION\_WAKE\_REASON**](https://msdn.microsoft.com/library/windows/hardware/dn897834)

 

 






