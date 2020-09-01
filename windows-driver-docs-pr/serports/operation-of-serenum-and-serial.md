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
ms.openlocfilehash: 6f6d24bf5afc893896a785970ee989da2aac8434
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186967"
---
# <a name="operation-of-serenum-and-serial"></a>Serenum 和串行的操作

本部分包括有关 Serenum 和串行操作的以下主题：

[对 I/O 请求进行 Serenum 筛选](serenum-filtering-of-i-o-requests.md)

[枚举 Serenum 设备](enumerating-serenum-devices.md)

[枚举旧版 COM 端口](enumerating-legacy-com-ports.md)

[COM 端口的外部命名](external-naming-of-com-ports.md)

[打开并初始化串行设备](opening-and-initializing-a-serial-device.md)

[打开并初始化 16550 UART 兼容接口](opening-and-initializing-a-16550-uart-compatible-interface.md)

[共享串行设备中断](sharing-a-serial-device-interrupt.md)

[启动串行设备](powering-up-a-serial-device.md)

[设置串行设备的读取和写入超时](setting-read-and-write-timeouts-for-a-serial-device.md)

[删除 RS-232 端口上的即插即用串行设备](removing-a-plug-and-play-serial-device-on-an-rs-232-port.md)

[删除即插即用 RS-232 端口](removing-a-plug-and-play-rs-232-port.md)

[串行设备控制请求](serial-device-control-requests2.md)

[确定调试程序使用哪个 COM 端口](determining-which-com-port-a-debugger-uses.md)

有关操作 Serenum 和串行的详细信息，请参阅以下资源：

- [ntddser 标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/0)

- [串行端口驱动程序参考](/windows-hardware/drivers/ddi/_serports/)

- \\ \\ \\ \\ \\ \\ Windows 驱动程序工具包 (WDK) 中的源内核串行和 src 内核 serenum 目录中的示例代码https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serenum

- Microsoft Windows SDK 中的 Windows 基础服务支持的通信资源