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
ms.openlocfilehash: 8d7502aa337e0615baf215edc54ec96173335bb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348539"
---
# <a name="minidriver-initialization"></a>微型驱动程序初始化





当操作系统首次初始化微型驱动程序时，它将调用微型驱动程序的**DriverEntry**例程。 请参阅[ **Stream 类微型驱动程序的 DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff558717)。 微型驱动程序必须注册自身的类驱动程序通过调用[ **StreamClassRegisterMinidriver**](https://msdn.microsoft.com/library/windows/hardware/ff568263)。

微型驱动程序传递[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构，它为类驱动程序提供了初步信息，包括设备级回调，[ *StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)， [ *StrMiniCancelPacket*](https://msdn.microsoft.com/library/windows/hardware/ff568448)， [ *StrMiniRequestTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff568473)，并[ *StrMiniInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff568459)。

在类驱动程序然后使用[ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)以指示它应初始化设备微型驱动程序。 它将发送 SRB\_初始化\_设备的请求，并将传递[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567785)与所需的结构硬件信息。 微型驱动程序时完成此请求，提供以字节为单位的大小[ **HW\_流\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff559686)结构，它用来描述所有其流。

在类驱动程序微型驱动程序完成该请求，使用[ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)发送 SRB\_获取\_流\_信息请求。 然后，微型驱动程序提供了有关其流，包括每个流的回调的所有信息。

完成的类驱动程序处理流数据后，它使用[ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)发送 SRB\_初始化\_完整的请求。 此时，微型驱动程序已准备好开始处理请求上每个流。

 

 




