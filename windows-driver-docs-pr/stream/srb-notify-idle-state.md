---
title: SRB\_通知\_空闲\_状态
description: 在类驱动程序发送的第一次打开请求或最后一个的关闭请求之前立即将此请求发送到微型驱动程序。 微型驱动程序可以使用 SRB\_通知\_空闲\_作为通知唤醒从 USB 选择性挂起状态。
ms.assetid: 7a2950a4-bd9f-4765-bb60-9e3aeeff49fb
keywords:
- SRB_NOTIFY_IDLE_STATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_NOTIFY_IDLE_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8532033ea5d2988db5ebb212efc5a31bcd75115f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522532"
---
# <a name="srbnotifyidlestate"></a>SRB\_通知\_空闲\_状态


在类驱动程序发送的第一次打开请求或最后一个的关闭请求之前立即将此请求发送到微型驱动程序。 微型驱动程序可以使用 SRB\_通知\_IDLE\_状态的通知，以便从唤醒作为[USB 选择性挂起](../usbcon/usb-selective-suspend.md)。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

此请求是通知数据包仅;将忽略任何微型驱动程序提供的返回值。

<a name="remarks"></a>备注
-------

SRB\_通知\_空闲\_中 Microsoft Windows XP Service Pack 2 (SP2) 和更高版本，但在 Microsoft Windows Server 2003 中不发送状态。

SRB\_通知\_IDLE\_状态修补程序 USB 选择性挂起的流类驱动程序中存在的问题 (*Stream.sys*) 在 Windows XP sp1 中中, 所述[知识文章 813348](https://go.microsoft.com/fwlink/p/?linkid=210855)。 可以使用 SRB\_通知\_IDLE\_状态，以便支持选择性挂起单个实例的微型驱动程序基于中[流式传输类](https://msdn.microsoft.com/library/windows/hardware/ff568277)并[USBCAMD2](https://msdn.microsoft.com/library/windows/hardware/ff568573)。

在 Windows XP 及更早版本，SRB\_通知\_空闲\_状态不存在。 对于 Windows XP 及更早版本，微型驱动程序收到[ **SRB\_获取\_设备\_属性**](srb-get-device-property.md)从空闲状态唤醒。 然后调用微型驱动程序[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)设备状态更改为 D0。

在 Windows XP SP1 和 Windows Server 2003，SRB\_获取\_设备\_属性不在此情况下发送。 如果使用的*Stream.sys*使用这些操作系统，请按照前面提到的知识库文章中的说明。

当打开设备的第一个实例，在类驱动程序将发送 SRB\_通知\_IDLE\_之前发送的状态[ **SRB\_打开\_设备\_实例**](srb-open-device-instance.md)。

当关闭设备的最后一个实例，在类驱动程序将发送 SRB\_通知\_空闲\_状态之前为该设备将请求发送到转换到状态 D3。

当流类驱动程序发送 SRB\_通知\_IDLE\_状态请求，微型驱动程序将接收到调用[ *StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)。

## <a name="see-also"></a>另请参阅


[**SRB\_GET\_DEVICE\_PROPERTY**](srb-get-device-property.md)

[**SRB\_开放\_设备\_实例**](srb-open-device-instance.md)

[*StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)

 

 






