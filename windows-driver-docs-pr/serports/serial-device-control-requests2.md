---
title: 串行设备控制请求
description: 串行设备控制请求
keywords:
- 串行设备 WDK，设备控制请求
- 设备控制请求 WDK 串行设备
- 串行驱动程序 WDK，设备控制请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8455c77534ada18beddf184136181c9a78b1dadf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804959"
---
# <a name="serial-device-control-requests"></a>串行设备控制请求

串行提供设备控制请求来控制支持 16550 UART 兼容接口的串行设备的操作。

串行支持客户端可用于执行以下任务的 **IOCTL \_ 串行 \_ XXX** 请求：

- 获取和设置控制寄存器和控制信号。

- 获取并设置线条控件和调制解调器控件。

- 设置 FIFO 控件。

- 获取并设置握手和流控制操作和参数。

- 获取并设置等待事件。

- 清除内部缓冲区，设置接收缓冲区大小，然后重置设备。

- 获取和设置用于读取和写入请求的超时。

- 获取和清除性能统计信息。

- 获取状态信息。

- 获取设备的属性。

串行支持受信任的内核模式客户端可用于执行以下任务的 **IOCTL \_ 串行 \_ 内部 \_ XXX** 请求：

- 设置设备上的基本设置并还原以前的设置。

- 禁用和启用设备的等待/唤醒操作。

有关 [COM 端口](configuration-of-com-ports.md)的高级操作的详细信息，请参阅 Microsoft Windows SDK 中 Windows 基础服务支持的通信资源的相关信息。

有关串行 i/o 请求的详细信息，请参阅 [串行端口](/windows-hardware/drivers/ddi/_serports/) 参考主题。

有关 IOCTL \_ 串行 \_ XXX 和 ioctl \_ 串行内部 XXX 请求的详细信息， \_ \_ 请参阅 [ntddser](/windows-hardware/drivers/ddi/ntddser/) 标头。
