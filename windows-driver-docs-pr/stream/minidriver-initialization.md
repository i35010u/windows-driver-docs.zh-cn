---
title: 微型驱动程序初始化
description: 微型驱动程序初始化
ms.assetid: 5aa4e2c6-5848-45fe-8a89-686aae7e85e6
keywords:
- 初始化流式处理微型驱动程序 WDK Windows 2000 内核
- Stream.sys 类驱动程序 WDK Windows 2000 内核，初始化微型驱动程序
- 流式处理微型驱动程序 WDK Windows 2000 内核，初始化
- 微型驱动程序 WDK Windows 2000 内核流式处理，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b342ce22bf19d69aa5439c0be646a5c5f734556c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363299"
---
# <a name="minidriver-initialization"></a>微型驱动程序初始化





当操作系统首次初始化微型驱动程序时，它将调用微型驱动程序的**DriverEntry**例程。 请参阅[ **Stream 类微型驱动程序的 DriverEntry**](https://docs.microsoft.com/previous-versions/ff558717(v=vs.85))。 微型驱动程序必须注册自身的类驱动程序通过调用[ **StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisteradapter)。

微型驱动程序传递[ **HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)结构，它为类驱动程序提供了初步信息，包括设备级回调，[ *StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)， [ *StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_cancel_srb)， [ *StrMiniRequestTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_request_timeout_handler)，并[ *StrMiniInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_interrupt)。

在类驱动程序然后使用[ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)以指示它应初始化设备微型驱动程序。 它将发送 SRB\_初始化\_设备的请求，并将传递[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_port_configuration_information)与所需的结构硬件信息。 微型驱动程序时完成此请求，提供以字节为单位的大小[ **HW\_流\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)结构，它用来描述所有其流。

在类驱动程序微型驱动程序完成该请求，使用[ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)发送 SRB\_获取\_流\_信息请求。 然后，微型驱动程序提供了有关其流，包括每个流的回调的所有信息。

完成的类驱动程序处理流数据后，它使用[ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)发送 SRB\_初始化\_完整的请求。 此时，微型驱动程序已准备好开始处理请求上每个流。

 

 




