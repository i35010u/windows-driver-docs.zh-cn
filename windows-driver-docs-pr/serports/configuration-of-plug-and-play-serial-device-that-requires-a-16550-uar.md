---
title: 即插即用串行设备配置为 16550 UART 接口
description: Plug and Play 串行设备 16550 UART 兼容接口所需的配置
ms.assetid: b99259bd-7573-4f71-9ab5-b263eed41288
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，插
- 通用的异步接收方发射机 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容接口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d33022330c634889e371ed428c898d702098eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533147"
---
# <a name="configuration-of-plug-and-play-serial-device-that-requires-a-16550-uart-compatible-interface"></a>Plug and Play 串行设备 16550 UART 兼容接口所需的配置





本部分介绍用于串行设备的硬件、 驱动程序和设备堆栈的典型配置的：

-   支持即插。

-   需要 16550 UART 兼容接口。

-   未连接到 RS-232 端口。

例如，使用调制解调器的 PCMCIA 卡。

下图显示了示例 toaster 设备和需要 16550 UART 兼容界面示例 blender 设备的典型配置。

![左的图： pcmcia 卡上的插 toaster 设备的硬件配置。 右图： 驱动程序和 pcmcia 卡上的插 toaster 设备的设备堆栈的配置](images/ser3.png)

在这些配置 Toaster 设备是 PCMCIA 总线上的子设备。 PCMCIA 总线驱动程序创建 Toaster 设备 PDO 时枚举 PCMCIA 卡。 Toaster 设备的 INF 文件指定为较低级别设备筛选器驱动程序的序列。 序列提供硬件设备 16550 UART 兼容接口。 Toaster 驱动程序创建，并将 FDO 附加到 Toaster 设备堆栈。

 

 




