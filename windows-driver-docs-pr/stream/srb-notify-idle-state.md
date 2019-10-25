---
title: SRB\_通知\_空闲\_状态
description: 类驱动程序会在发送第一个打开请求或最后一个关闭请求之前立即将此请求发送到微型驱动程序。 微型驱动程序可以使用 SRB\_通知\_空闲\_状态，作为从 USB 选择性挂起唤醒的通知。
ms.assetid: 7a2950a4-bd9f-4765-bb60-9e3aeeff49fb
keywords:
- SRB_NOTIFY_IDLE_STATE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_NOTIFY_IDLE_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c9b85da8423269f8761a00e8ed2402cf7d41815
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843294"
---
# <a name="srb_notify_idle_state"></a>SRB\_通知\_空闲\_状态


类驱动程序会在发送第一个打开请求或最后一个关闭请求之前立即将此请求发送到微型驱动程序。 微型驱动程序可以使用 SRB\_通知\_空闲\_状态，作为从[USB 选择性挂起](../usbcon/usb-selective-suspend.md)唤醒的通知。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

此请求仅为通知数据包;将忽略任何微型驱动程序提供的返回值。

<a name="remarks"></a>备注
-------

在 Microsoft windows XP Service Pack 2 （SP2）和更高版本（但不是在 Microsoft Windows Server 2003 中）发出的 SRB\_通知\_空闲\_状态。

SRB\_通知\_空闲\_状态修复了 Windows XP SP1 （在 Windows XP SP1*中）中*存在的 USB 选择性挂起问题，如[知识库文章 813348](https://go.microsoft.com/fwlink/p/?linkid=210855)中所述。 您可以使用 SRB\_通知\_空闲\_状态，以支持在基于[流类](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)和[USBCAMD2](https://docs.microsoft.com/windows-hardware/drivers/stream/usbcamd2-minidriver-operation)的单一实例微型驱动程序内进行选择性挂起。

在 Windows XP 及更早版本中，SRB\_通知\_空闲\_状态不存在。 对于 Windows XP 和更早版本，微型驱动程序接收[**SRB\_获取\_设备\_属性**](srb-get-device-property.md)以从空闲状态唤醒。 然后，微型驱动程序调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)将设备状态更改为 D0。

在 Windows XP SP1 和 Windows Server 2003 中，在这种情况下，SRB\_获取\_设备\_属性未发送。 如果使用的是包含这些操作系统的*sys.databases* ，请按照前面提到的知识库文章中的说明进行操作。

打开设备的第一个实例时，类驱动程序会立即发送 SRB\_通知\_空闲\_状态，然后再发送[**SRB\_打开\_设备\_实例**](srb-open-device-instance.md)。

关闭设备的最后一个实例时，类驱动程序将发送 SRB\_在发送设备请求以便转换到状态 D3 之前立即通知\_空闲\_状态。

当 stream 类驱动程序发送 SRB\_通知\_IDLE\_状态请求时，微型驱动程序将接收对[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)的调用。

## <a name="see-also"></a>另请参阅


[**SRB\_获取\_设备\_属性**](srb-get-device-property.md)

[**SRB\_打开\_设备\_实例**](srb-open-device-instance.md)

[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)

 

 






