---
title: 访问 PCMCIA 设备的属性内存
description: 访问 PCMCIA 设备的属性内存
keywords:
- PCMCIA WDK 总线，属性内存
- 属性内存 WDK PCMCIA 总线
- 属性内存 WDK PCMCIA 总线，关于属性内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018459be387bb3b887e7ff74fc15e22e0a2768fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812535"
---
# <a name="access-attribute-memory-of-a-pcmcia-device"></a>访问 PCMCIA 设备的属性内存





本部分介绍了 Microsoft Windows 2000 和更高版本操作系统中的 PCMCIA 设备驱动程序如何可以访问 PCMCIA 设备的属性内存：

-   [访问 PCMCIA 设备的属性内存的要求](./requirements-for-accessing-attribute-memory-of-a-pcmcia-device.md)

-   [使用即插即用 I/O 请求访问 PCMCIA 属性内存](./access-pcmcia-attribute-memory-by-using-a-plug-and-play-i-o-request.md)

    这是一种非常适合大多数用途的简单方法，但只能以 IRQL &lt; 调度级别运行 \_ 。

-   [使用总线 \_ 接口标准界面访问 PCMCIA 属性内存 \_](./access-pcmcia-attribute-memory-by-using-a-bus-interface-standard-inter.md)

    此方法可消除 i/o 请求的开销，并可运行 IRQL &lt; = 调度 \_ 级别

-   [通过永久内存窗口访问 PCMCIA 属性内存](./access-pcmcia-attribute-memory-through-a-permanent-memory-window.md)

    驱动程序的 ISR 可以使用此方法在 IRQL DIRQL 运行时直接访问内存。

-   [使用 PCMCIA \_ 接口标准界面访问 Pcmcia 属性内存 \_](./access-pcmcia-attribute-memory-by-using-a-pcmcia-interface-standard-in.md)

    内存卡驱动程序可以使用以下方法： IRQL &lt; = 调度 \_ 级别。

*pcmcia.sys*，在 Windows 2000 和更高版本的操作系统中，PCMCIA 总线的系统驱动程序支持这些方法。

 

