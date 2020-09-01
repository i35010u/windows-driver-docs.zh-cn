---
title: SRB \_ 通知 \_ 空闲 \_ 状态
description: 类驱动程序会在发送第一个打开请求或最后一个关闭请求之前立即将此请求发送到微型驱动程序。 微型驱动程序可以使用 SRB \_ 通知 \_ 空闲 \_ 状态作为从 USB 选择性挂起唤醒的通知。
ms.assetid: 7a2950a4-bd9f-4765-bb60-9e3aeeff49fb
keywords:
- SRB_NOTIFY_IDLE_STATE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_NOTIFY_IDLE_STATE
api_type:
- NA
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: aef0b4d0f6bc8ab4acb2b0593730c83e28c2c58a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189929"
---
# <a name="srb_notify_idle_state"></a>SRB \_ 通知 \_ 空闲 \_ 状态

类驱动程序会在发送第一个打开请求或最后一个关闭请求之前立即将此请求发送到微型驱动程序。 微型驱动程序可以使用 SRB \_ 通知 \_ 空闲 \_ 状态作为从 [USB 选择性挂起](../usbcon/usb-selective-suspend.md)唤醒的通知。

## <a name="return-value"></a>返回值

此请求仅为通知数据包;将忽略任何微型驱动程序提供的返回值。

## <a name="remarks"></a>备注

SRB \_ 通知 \_ 空闲 \_ 状态在 Microsoft Windows XP Service PACK 2 (SP2) 和更高版本，但在 microsoft windows Server 2003 中发送。

SRB \_ 通知 \_ 空闲 \_ 状态修复了 stream 类驱动程序中存在的 USB 选择性挂起问题， (*Stream.sys* Windows XP SP1 中的) 。 你可以使用 SRB \_ 通知 \_ 空闲 \_ 状态，以便在基于 [流类](./streaming-minidrivers2.md) 和 [USBCAMD2](./usbcamd2-minidriver-operation.md)的单一实例微型驱动程序中支持选择性挂起。

在 Windows XP 及更早版本中，SRB \_ 通知 \_ 空闲 \_ 状态不存在。 对于 Windows XP 和更早版本，微型驱动程序接收 [**SRB \_ 获取 \_ 设备 \_ 属性**](srb-get-device-property.md) 以从空闲状态唤醒。 然后，微型驱动程序调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 将设备状态更改为 D0。

在 Windows XP SP1 和 Windows Server 2003 中， \_ \_ \_ 在这种情况下不会发送 SRB 获取设备属性。 如果将 *Stream.sys* 与这些操作系统一起使用，请按照前面提到的知识库文章中的说明进行操作。

打开设备的第一个实例时，类驱动程序会在 \_ \_ \_ 发送 [**SRB \_ 打开 \_ 设备 \_ 实例**](srb-open-device-instance.md)之前立即发送 SRB 通知空闲状态。

关闭设备的最后一个实例时，类驱动程序会在 \_ \_ \_ 发送设备请求以过渡到状态 D3 之前立即发送 SRB 通知空闲状态。

当 stream 类驱动程序发送 SRB \_ 通知 \_ 空闲 \_ 状态请求时，微型驱动程序将接收对 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)的调用。

## <a name="see-also"></a>另请参阅

[**SRB \_ 获取 \_ 设备 \_ 属性**](srb-get-device-property.md)

[**SRB \_ 打开 \_ 设备 \_ 实例**](srb-open-device-instance.md)

[*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)