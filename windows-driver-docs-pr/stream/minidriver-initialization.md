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
ms.openlocfilehash: 481dc1023ab1358ac7ed4d275dcf7680d49eda01
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185859"
---
# <a name="minidriver-initialization"></a>微型驱动程序初始化





当操作系统首次初始化微型驱动程序时，它将调用微型驱动程序的 **DriverEntry** 例程。 请参阅 [**Stream 类微型驱动程序的 DriverEntry**](/previous-versions/ff558717(v=vs.85))。 微型驱动程序必须通过调用 [**StreamClassRegisterMinidriver**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)向类驱动程序注册自身。

微型驱动程序传递了一个 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data) 结构，该结构为类驱动程序提供了初步信息，其中包括设备范围的回调、 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)、 [*StrMiniCancelPacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb)、 [*StrMiniRequestTimeout*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)和 [*StrMiniInterrupt*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_interrupt)。

然后，类驱动程序使用 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) 向微型驱动程序发出信号，指示它应该初始化设备。 它将发送 SRB \_ 初始化 \_ 设备请求，并向 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_port_configuration_information) 结构传递所需的硬件信息。 完成此请求时，微型驱动程序提供了 [**HW \_ 流 \_ 描述符**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor) 结构的大小（以字节为单位），该结构用于描述其所有流。

微型驱动程序完成该请求后，类驱动程序将使用 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) 来发送 SRB \_ 获取 \_ 流 \_ 信息请求。 然后，微型驱动程序提供其所有流的相关信息，包括每个流的回调。

类驱动程序完成处理流数据后，它将使用 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) 发送 SRB \_ 初始化 \_ 完成请求。 此时，微型驱动程序已准备好开始处理每个流上的请求。

 

