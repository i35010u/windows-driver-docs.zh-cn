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
ms.openlocfilehash: f3bd13858c56d71b65443e3858ef418df7e94dde
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836324"
---
# <a name="serial-device-control-requests"></a>串行设备控制请求

序列提供了设备控制请求，以控制支持 16550 UART 兼容接口的串行设备的操作。

支持串行**IOCTL\_串行\_XXX**请求客户端可用来执行以下任务：

- Get 和 set 控制寄存器和控制信号。

- 获取和设置行控制和调制解调器控制。

- 设置先进先出控制。

- 获取和设置握手和流控制操作和参数。

- 获取和设置等待事件。

- 清除内部缓冲区中，设置接收缓冲区的大小，并将设备重置。

- 获取和设置用于读取和写入请求的超时。

- 获取并清除性能统计信息。

- 获取状态信息。

- 获取设备的属性。

支持串行**IOCTL\_串行\_内部\_XXX**请求受信任的内核模式下客户端可用来执行以下任务：

- 在设备上设置基本设置和还原以前的设置。

- 禁用和启用设备的等待/唤醒操作。

有关高级操作的详细信息[COM 端口](configuration-of-com-ports.md)，请参阅支持的 Microsoft Windows SDK 中的 Windows 基本服务的通信资源有关的信息。

有关串行 I/O 请求的详细信息，请参阅[串行端口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_serports/)参考主题。

详细了解 IOCTL\_串行\_XXX 和 IOCTL\_串行\_内部\_XXX 请求，请参阅[ntddser.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ntddser/)标头。
