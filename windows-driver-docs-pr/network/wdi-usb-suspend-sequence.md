---
title: WDI USB 挂起序列
description: 当 NDIS 检测到空闲时间超过选择性挂起空闲超时（SSIdleTimeout）时，NDIS 将调用 UE。
ms.assetid: EEDA274F-AC7D-4515-BAAF-FBEDDF95D2DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414a7b54feb02498e6615d0bfebecb8f91f916f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841711"
---
# <a name="wdi-usb-suspend-sequence"></a>WDI USB 挂起序列


当 NDIS 检测到空闲时间超过选择性挂起空闲超时（*SSIdleTimeout*）时，ndis 将调用 UE。 UE 可以通过返回 NDIS\_状态\_繁忙来拒绝空闲通知。 如果 UE 不拒绝空闲通知，则 UE 将通过**LeIdleNotificationHander**调用 le，并且该 le 可能会被拒绝或接受。

如果没有挂起的数据、命令或计时器（将数据或命令向下发送到 LE），则 UE 会接受空闲通知。

当 WDI 收到 D2 OID 时，它将处理 OID，就像它是常规的 D2 一样，只是它将 WDI OID 连同原因代码设置为**WDI\_设置\_POWER\_DX\_原因\_SELETIVE\_挂起**

下面的流程图显示了挂起的序列。

![wdi usb 挂起顺序](images/wdi-usb-suspend-sequence-flow.png)

## <a name="related-topics"></a>相关主题


[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

[**WDI\_TLV\_设置\_POWER\_DX\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-power-dx-reason)

 

 






