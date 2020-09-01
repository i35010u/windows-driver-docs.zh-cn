---
title: 串行和 Serenum 的功能
description: 串行和 Serenum 的功能
ms.assetid: 47202203-935a-4e1a-9b05-5555f7cbcfa8
keywords:
- 串行设备 WDK，串行驱动程序
- 串行设备 WDK，Serenum 驱动程序
- 串行驱动程序 WDK，关于串行驱动程序
- Serenum driver WDK，关于 Serenum 驱动程序
- 串行服务 WDK
- 串行驱动程序 WDK
ms.date: 04/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: b8ef6670f818971c2e992f23c94cd6abd92bb5b8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187003"
---
# <a name="features-of-serial-and-serenum"></a>串行和 Serenum 的功能





从 Windows 2000 开始，系统提供的 Serial.sys 和 Serenum.sys 驱动程序可用于管理串行控制器设备，这些设备具有与16550通用异步接收器-发射器 (UART) 兼容的硬件接口。 Serial.sys 控制独立串行端口、COM 端口和多端口板。 Serenum.sys 枚举连接到串行端口的设备，该串行端口由 Serial.sys 或兼容的串行驱动程序控制。

有关 SerCx2 和 SerCx 的 Serial.sys 的比较，请参阅 [串行控制器驱动程序概述](serial-drivers-overview.md)。 SerCx2 从 Windows 8.1 开始可用。 从 Windows 8 开始可以使用 SerCx。

串行实现串行服务;它的可执行映像是 Serial.sys。

串行用于：

-   旧式和即插即用串行设备的函数驱动程序。

-   需要 16550 UART 兼容接口的即插即用设备的低级设备筛选器驱动程序。 [PCMCIA 总线](../pcmcia/index.md)上的调制解调器就是此配置的一个示例。

    作为筛选器驱动程序的串行操作的操作与其作为函数驱动程序的操作相同。

串行功能如下：

-    (WMI) 即插即用、电源管理和 Windows Management Instrumentation。

-   串行设备堆栈的电源策略所有者，包括串行设备。

-   支持无数个独立串行端口、 [COM 端口](configuration-of-com-ports.md)和多端口板。

-   控制中断和与设备硬件的通信。

Serenum 实现 Serenum 服务;它的可执行映像是 Serenum.sys。

Serenum 是一个上层设备筛选器驱动程序，与串行端口功能驱动程序一起用于枚举连接到串行端口的下列设备类型：

-   符合 *即插即用外部 COM 设备规范的即插即用串行设备，版本1.00，年2月 28 1995 日*。

-   在 Microsoft Windows NT 4.0 及更早版本中符合旧版鼠标检测的指针设备。

串行和 Serenum 的组合操作为串行端口提供即插即用总线驱动程序的功能。

Serenum 支持即插即用和电源管理。

Serenum 不支持 Windows 驱动模型，只应在 Windows 2000 和更高版本中使用。

从 Windows 2000 开始，Serenum 支持串行端口和其他需要枚举串行端口的串行端口函数驱动程序。 硬件供应商不必为串行端口创建自己的枚举器。 例如，设备驱动程序可以使用 Serenum 来枚举连接到多端口设备上的单个串行端口的设备。

 

