---
title: WDI USB 挂起序列
description: 当 NDIS 检测到空闲的时间超过的选择性挂起的空闲超时 (SSIdleTimeout) 时，NDIS 调用下，用户设备。
ms.assetid: EEDA274F-AC7D-4515-BAAF-FBEDDF95D2DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46c19fa7d9aab8224ad2fc992749694dcdc97967
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357096"
---
# <a name="wdi-usb-suspend-sequence"></a>WDI USB 挂起序列


当 NDIS 检测到空闲的时间超过的选择性挂起的空闲超时值 (*SSIdleTimeout*)、 NDIS 调用下，用户设备。 UE 可能通过返回 NDIS 来禁止空闲通知\_状态\_忙。 UE 下，用户设备不能阻止空闲通知，如果调用使用 LE **LeIdleNotificationHander**，和 LE 可能能否决或接受。

在没有任何挂起的数据、 命令或发送数据或向下 LE 命令可能会过期的计时器时，UE 接受空闲通知。

当 WDI 收到 D2 OID 时，它处理 OID 如同它是正则 D2，只不过它将设置为，原因代码发送 WDI OID **WDI\_设置\_POWER\_DX\_原因\_SELETIVE\_挂起**。

以下流程图显示挂起序列。

![wdi usb 挂起序列](images/wdi-usb-suspend-sequence-flow.png)

## <a name="related-topics"></a>相关主题


[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

[**WDI\_TLV\_SET\_POWER\_DX\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-power-dx-reason)

 

 






