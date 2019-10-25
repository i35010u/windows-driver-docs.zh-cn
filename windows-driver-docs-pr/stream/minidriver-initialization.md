---
title: 微型驱动程序初始化
description: 微型驱动程序初始化
ms.assetid: 5aa4e2c6-5848-45fe-8a89-686aae7e85e6
keywords:
- 初始化流式处理微型驱动程序 WDK Windows 2000 内核
- Stream .sys 类驱动程序 WDK Windows 2000 内核，初始化微型驱动程序
- 流式处理微型驱动程序 WDK Windows 2000 内核，初始化
- 微型驱动程序 WDK Windows 2000 内核流式处理，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e561bfc937c39a9d4987a754ad2b7ecd236b3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842134"
---
# <a name="minidriver-initialization"></a>微型驱动程序初始化





当操作系统首次初始化微型驱动程序时，它将调用微型驱动程序的**DriverEntry**例程。 请参阅[**Stream 类微型驱动程序的 DriverEntry**](https://docs.microsoft.com/previous-versions/ff558717(v=vs.85))。 微型驱动程序必须通过调用[**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)向类驱动程序注册自身。

微型驱动程序[ **\_数据结构传递 HW\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)，它为类驱动程序提供初步信息，包括设备范围的回调、 [*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)、 [*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb)、 [*StrMiniRequestTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)和[*StrMiniInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_interrupt)。

然后，类驱动程序使用[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)向微型驱动程序发出信号，指示它应该初始化设备。 它将发送 SRB\_初始化\_设备请求，并使用所需的硬件信息向[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_port_configuration_information)结构。 完成此请求时，微型驱动程序将以字节为单位提供其用来描述其所有流的[**HW\_\_流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)的大小（以字节为单位）。

微型驱动程序完成该请求后，类驱动程序将使用[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)发送 SRB\_获取\_信息请求\_流。 然后，微型驱动程序提供其所有流的相关信息，包括每个流的回调。

类驱动程序处理完流数据后，将使用[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)将 SRB\_初始化发送\_完成请求。 此时，微型驱动程序已准备好开始处理每个流上的请求。

 

 




