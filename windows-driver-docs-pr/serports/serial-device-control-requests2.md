---
title: 串行设备控制请求
description: 串行设备控制请求
ms.assetid: 12dab038-e4da-47b5-ada8-e1c7ee980cde
keywords:
- 串行设备 WDK，设备控制请求
- 设备控制请求 WDK 串行设备
- 串行驱动程序 WDK，设备控制请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e55a2fe562876c41ddc1ff34dab7732f278cad0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845393"
---
# <a name="serial-device-control-requests"></a>串行设备控制请求

串行提供设备控制请求来控制支持 16550 UART 兼容接口的串行设备的操作。

串行支持**IOCTL\_串行\_XXX**请求，客户端可以使用这些请求来执行以下任务：

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

串行支持**IOCTL\_串行\_内部\_XXX**请求，可信内核模式客户端可以使用这些请求来执行以下任务：

- 设置设备上的基本设置并还原以前的设置。

- 禁用和启用设备的等待/唤醒操作。

有关[COM 端口](configuration-of-com-ports.md)的高级操作的详细信息，请参阅 Microsoft Windows SDK 中 Windows 基础服务支持的通信资源的相关信息。

有关串行 i/o 请求的详细信息，请参阅[串行端口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_serports/)参考主题。

若要详细了解 IOCTL\_串行\_XXX 和 IOCTL\_串行\_内部\_XXX 请求，请参阅[ntddser](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/ntddser/)标头。
