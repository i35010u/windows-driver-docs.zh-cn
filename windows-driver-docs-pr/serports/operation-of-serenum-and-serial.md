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
ms.openlocfilehash: 58cb5c8b89eae23ddfb3742f7a6b20222bed9403
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837971"
---
# <a name="operation-of-serenum-and-serial"></a>Serenum 和串行的操作

本部分包括有关 Serenum 和串行操作的以下主题：

[Serenum 对 i/o 请求的筛选](serenum-filtering-of-i-o-requests.md)

[枚举 Serenum 设备](enumerating-serenum-devices.md)

[枚举旧 COM 端口](enumerating-legacy-com-ports.md)

[COM 端口的外部命名](external-naming-of-com-ports.md)

[打开和初始化串行设备](opening-and-initializing-a-serial-device.md)

[打开并初始化 16550 UART 兼容的接口](opening-and-initializing-a-16550-uart-compatible-interface.md)

[共享串行设备中断](sharing-a-serial-device-interrupt.md)

[打开串行设备](powering-up-a-serial-device.md)

[设置串行设备的读取和写入超时](setting-read-and-write-timeouts-for-a-serial-device.md)

[删除 RS-232 端口上的即插即用串行设备](removing-a-plug-and-play-serial-device-on-an-rs-232-port.md)

[删除即插即用 RS-232 端口](removing-a-plug-and-play-rs-232-port.md)

[串行设备控制请求](serial-device-control-requests2.md)

[确定调试器使用的 COM 端口](determining-which-com-port-a-debugger-uses.md)

有关操作 Serenum 和串行的详细信息，请参阅以下资源：

- [ntddser 标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/0)

- [串行端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_serports/)

- Windows 驱动程序工具包（WDK）中的 \\src 中的示例代码\\内核\\串行和 \\src\\内核\\serenum 目录 https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serenum

- Microsoft Windows SDK 中的 Windows 基础服务支持的通信资源
