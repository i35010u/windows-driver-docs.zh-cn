---
title: 串行和 Serenum 的功能
description: 串行和 Serenum 的功能
ms.assetid: 47202203-935a-4e1a-9b05-5555f7cbcfa8
keywords:
- 串行设备 WDK，串行驱动程序
- 串行设备 WDK，Serenum 驱动程序
- 串行驱动程序 WDK，有关串行驱动程序
- Serenum 驱动程序 WDK，有关 Serenum 驱动程序
- 串行服务 WDK
- 串行驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c0095d082663c70cbdb3158c5304054396b2433
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380002"
---
# <a name="features-of-serial-and-serenum"></a>串行和 Serenum 的功能





从 Windows 2000 开始，系统提供 Serial.sys 和 Serenum.sys 驱动程序都可用于管理具有与 16550 通用异步收发-器 (UART) 兼容的硬件接口的串行控制器设备。 Serial.sys 控制独立串行端口、 COM 端口和多端口的板。 Serenum.sys 枚举到由 Serial.sys 或兼容的串行驱动程序控制的串行端口连接的设备。

有关比较 Serial.sys 至串行 framework 的扩展，SerCx2 和 SerCx，请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)。 可从 Windows 8.1 SerCx2。 可从 Windows 8 开始 SerCx。

串行实现串行服务;其可执行文件映像是 Serial.sys。

用作序列：

-   适用于旧版和插串行设备功能驱动程序。

-   Plug and Play 设备需要 16550 UART 兼容接口的较低级别设备筛选器驱动程序。 此配置的一个示例是上一个调制解调器[PCMCIA 总线](https://go.microsoft.com/fwlink/p/?LinkId=799534)。

    序列的操作筛选器驱动程序作为等同于其操作作为功能驱动程序。

序列具备以下功能：

-   Plug and Play、 电源管理和 Windows Management Instrumentation (WMI)。

-   包含序列的串行设备堆栈的电源策略所有者。

-   对无限数量的独立的串行端口的支持[COM 端口](configuration-of-com-ports.md)，和多端口的板。

-   控制中断和与设备硬件的通信。

Serenum 实现 Serenum 服务;其可执行文件映像是 Serenum.sys。

Serenum 是通过串行端口函数驱动程序中用于枚举以下类型的设备连接到串行端口的较高级别设备筛选器驱动程序：

-   即插即用串行设备是否符合*插外部 COM 设备规范，版本 1.00，1995 年 2 月 28 日，*。

-   符合 Microsoft Windows NT 4.0 和更早版本中的旧鼠标检测的指针设备。

序列和 Serenum 的组合的操作提供的串行端口插总线驱动程序的函数。

Serenum 支持插和电源管理。

Serenum 不支持 Windows 驱动程序模型，并应仅用于 Windows 2000 和更高版本。

从 Windows 2000 开始，Serenum 支持需要枚举串行端口的串行端口和其他串行端口函数驱动程序。 硬件供应商不需要创建其自己的串行端口的枚举器。 例如，设备驱动程序可以使用 Serenum 枚举附加到多个端口的设备上的单个串行端口的设备。

 

 




