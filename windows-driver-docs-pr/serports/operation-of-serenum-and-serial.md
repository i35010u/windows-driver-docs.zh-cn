---
title: Serenum 和串行的操作
description: Serenum 和串行的操作
ms.assetid: d14b6655-c031-42dd-921e-b6a09afde86d
keywords:
- 串行驱动程序 WDK，操作
- Serenum 驱动程序 WDK，操作
- 串行驱动程序 WDK
- Serenum 驱动程序 WDK
- 串行驱动程序 WDK
- 串行设备 WDK，串行驱动程序
- 串行设备 WDK，Serenum 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64ddc6f95f6950807b5d18eb0b05d07814da8adf
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836346"
---
# <a name="operation-of-serenum-and-serial"></a>Serenum 和串行的操作

本部分包括有关操作系统 Serenum 和序列的以下主题：

[Serenum 筛选的 I/O 请求](serenum-filtering-of-i-o-requests.md)

[枚举 Serenum 设备](enumerating-serenum-devices.md)

[枚举旧 COM 端口](enumerating-legacy-com-ports.md)

[外部命名的 COM 端口](external-naming-of-com-ports.md)

[打开并初始化串行设备](opening-and-initializing-a-serial-device.md)

[打开并初始化 16550 UART 兼容接口](opening-and-initializing-a-16550-uart-compatible-interface.md)

[共享串行设备中断](sharing-a-serial-device-interrupt.md)

[启动串行设备](powering-up-a-serial-device.md)

[设置读取和写入串行设备的超时](setting-read-and-write-timeouts-for-a-serial-device.md)

[RS-232 端口上的 Plug and Play 串行设备中删除](removing-a-plug-and-play-serial-device-on-an-rs-232-port.md)

[删除插 RS-232 端口](removing-a-plug-and-play-rs-232-port.md)

[串行设备控制请求](serial-device-control-requests2.md)

[确定哪个 COM 端口调试器使用](determining-which-com-port-a-debugger-uses.md)

有关操作系统 Serenum 和序列的详细信息，请参阅以下资源：

- [ntddser header](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/0)

- [串行端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_serports/)

- 示例中的代码\\src\\内核\\串行和\\src\\内核\\serenum 目录中 Windows Driver Kit (WDK) https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serenum

- 支持的 Microsoft Windows SDK 中的 Windows 基本服务的通信资源
