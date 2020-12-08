---
title: WDI USB 挂起序列
description: 当 NDIS 检测到空闲时间超过选择性挂起空闲超时 (SSIdleTimeout) 时，NDIS 将调用 UE。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ded4bd26646d44be095c5ccb1e620af3bcdf2b9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821915"
---
# <a name="wdi-usb-suspend-sequence"></a>WDI USB 挂起序列


当 NDIS 检测到空闲时间超过选择性挂起空闲超时 (*SSIdleTimeout*) 时，ndis 将调用 UE。 UE 可能会通过返回 NDIS 状态 "忙碌" 来否决空闲通知 \_ \_ 。 如果 UE 不拒绝空闲通知，则 UE 将通过 **LeIdleNotificationHander** 调用 le，并且该 le 可能会被拒绝或接受。

如果没有挂起的数据、命令或计时器（将数据或命令向下发送到 LE），则 UE 会接受空闲通知。

当 WDI 收到 D2 OID 时，它将处理 OID，就像它是常规的 D2 一样，只是它将发送 WDI OID，并将原因代码设置为 " **WDI \_ 设置 \_ POWER \_ DX \_ 原因 \_ SELETIVE \_ 挂起**"。

下面的流程图显示了挂起的序列。

![wdi usb 挂起顺序](images/wdi-usb-suspend-sequence-flow.png)

## <a name="related-topics"></a>相关主题


[*MiniportWdiIdleNotification*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

[**WDI \_ TLV \_ 设置 \_ POWER \_ DX \_ 原因**](./wdi-tlv-set-power-dx-reason.md)

 

