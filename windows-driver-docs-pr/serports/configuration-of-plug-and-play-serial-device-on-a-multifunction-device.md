---
title: 使用 16550 UART 界面配置即插即用的多功能串行设备
description: Plug and Play 串行设备需要 16550 UART 兼容接口的多功能设备上的配置
ms.assetid: 63588ac9-4c87-421d-8da3-3e950cbd466c
keywords:
- 即插即用串行设备 WDK
- 串行设备 WDK，插
- 通用的异步接收方发射机 WDK 串行设备
- UART WDK 串行设备
- 16550 UART 兼容接口 WDK 串行设备
- 多功能设备
- 多功能设备 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dce95ec1d57f8d591543b321a28a04b89402e84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545034"
---
# <a name="configuration-of-plug-and-play-serial-device-on-a-multifunction-device-that-requires-a-16550-uart-compatible-interface"></a>Plug and Play 串行设备需要 16550 UART 兼容接口的多功能设备上的配置





本部分介绍的多功能串行设备的硬件、 驱动程序和设备堆栈配置的：

-   支持即插。

-   需要 16550 UART 兼容接口。

-   未连接到 RS-232 端口。

一个具体的例子是让调制解调器，LAN 适配器 PCMCIA 卡。

下图显示了示例 toaster 设备和需要 16550 UART 兼容界面示例 blender 设备的典型配置

![演示如何硬件和驱动程序和设备堆栈配置 toaster 多功能 pcmcia 卡上，以及 toaster 和 blender 的关系图](images/ser4.png)

在这些配置 Toaster 设备是多功能设备上的子设备和多功能设备是子设备 PCMCIA 总线上。

INF 文件并为 Toaster 设备安装程序安装为较低级别设备筛选器驱动程序 Toaster 设备提供 16550 UART 兼容接口串行驱动程序。 Toaster 驱动程序创建，并将 FDO 附加到串行驱动程序筛选器执行操作。

 

 




