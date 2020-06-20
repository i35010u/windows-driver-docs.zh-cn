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
ms.openlocfilehash: 6d20d5db2658e6ce157ddca23d330b2fcbee24f9
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111242"
---
# <a name="srb_notify_idle_state"></a>SRB \_ 通知 \_ 空闲 \_ 状态

类驱动程序会在发送第一个打开请求或最后一个关闭请求之前立即将此请求发送到微型驱动程序。 微型驱动程序可以使用 SRB \_ 通知 \_ 空闲 \_ 状态作为从[USB 选择性挂起](../usbcon/usb-selective-suspend.md)唤醒的通知。

## <a name="return-value"></a>返回值

此请求仅为通知数据包;将忽略任何微型驱动程序提供的返回值。

## <a name="remarks"></a>备注

SRB \_ 通知 \_ 空闲 \_ 状态是在 Microsoft Windows XP Service PACK 2 （SP2）和更高版本中发送的，而不是在 microsoft windows Server 2003 中发送的。

SRB \_ 通知 \_ 空闲 \_ 状态修复 Windows XP SP1 中的 stream 类驱动程序（*Stream.sys*）中存在的 USB 选择性挂起问题。 你可以使用 SRB \_ 通知 \_ 空闲 \_ 状态，以便在基于[流类](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)和[USBCAMD2](https://docs.microsoft.com/windows-hardware/drivers/stream/usbcamd2-minidriver-operation)的单一实例微型驱动程序中支持选择性挂起。

在 Windows XP 及更早版本中，SRB \_ 通知 \_ 空闲 \_ 状态不存在。 对于 Windows XP 和更早版本，微型驱动程序接收[**SRB \_ 获取 \_ 设备 \_ 属性**](srb-get-device-property.md)以从空闲状态唤醒。 然后，微型驱动程序调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)将设备状态更改为 D0。

在 Windows XP SP1 和 Windows Server 2003 中， \_ \_ \_ 在这种情况下不会发送 SRB 获取设备属性。 如果将*Stream.sys*与这些操作系统一起使用，请按照前面提到的知识库文章中的说明进行操作。

打开设备的第一个实例时，类驱动程序会在 \_ \_ \_ 发送[**SRB \_ 打开 \_ 设备 \_ 实例**](srb-open-device-instance.md)之前立即发送 SRB 通知空闲状态。

关闭设备的最后一个实例时，类驱动程序会在 \_ \_ \_ 发送设备请求以过渡到状态 D3 之前立即发送 SRB 通知空闲状态。

当 stream 类驱动程序发送 SRB \_ 通知 \_ 空闲 \_ 状态请求时，微型驱动程序将接收对[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)的调用。

## <a name="see-also"></a>另请参阅

[**SRB \_ 获取 \_ 设备 \_ 属性**](srb-get-device-property.md)

[**SRB \_ 打开 \_ 设备 \_ 实例**](srb-open-device-instance.md)

[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)
