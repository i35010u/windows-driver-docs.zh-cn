---
title: 串行设备控制请求
description: 串行设备控制请求
ms.assetid: 12dab038-e4da-47b5-ada8-e1c7ee980cde
keywords:
- 串行设备 WDK、 设备控制请求
- 设备控制请求 WDK 串行设备
- 串行驱动程序 WDK、 设备控制请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e52ef3186cfdb820a35b9adfef079c7622a5de2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366513"
---
# <a name="serial-device-control-requests"></a>串行设备控制请求





序列提供了设备控制请求，以控制支持 16550 UART 兼容接口的串行设备的操作。

支持串行[IOCTL\_串行\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547466)请求客户端可用来执行以下任务：

-   Get 和 set 控制寄存器和控制信号。

-   获取和设置行控制和调制解调器控制。

-   设置先进先出控制。

-   获取和设置握手和流控制操作和参数。

-   获取和设置等待事件。

-   清除内部缓冲区中，设置接收缓冲区的大小，并将设备重置。

-   获取和设置用于读取和写入请求的超时。

-   获取并清除性能统计信息。

-   获取状态信息。

-   获取设备的属性。

支持串行[IOCTL\_串行\_内部\_Xxx](https://msdn.microsoft.com/library/windows/hardware/ff547480)请求受信任的内核模式下客户端可用来执行以下任务：

-   在设备上设置基本设置和还原以前的设置。

-   禁用和启用设备的等待/唤醒操作。

有关高级操作的详细信息[COM 端口](configuration-of-com-ports.md)，请参阅支持的 Microsoft Windows SDK 中的 Windows 基本服务的通信资源有关的信息。

有关串行 I/O 请求的详细信息，请参阅[串行驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff547476)。

 

 




