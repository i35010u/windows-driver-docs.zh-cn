---
title: 访问 PCMCIA 设备的属性内存
description: 访问 PCMCIA 设备的属性内存
ms.assetid: 270b8821-6322-4694-83eb-de319197dd6a
keywords:
- PCMCIA WDK 总线，属性内存
- 属性内存 WDK PCMCIA 总线
- 属性内存 WDK PCMCIA 总线，有关属性内存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca963b57979593242ee623ecbfd4e91f701875b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353536"
---
# <a name="access-attribute-memory-of-a-pcmcia-device"></a>访问 PCMCIA 设备的属性内存





本部分介绍如何在 Microsoft Windows 2000 和更高版本操作系统的 PCMCIA 设备的驱动程序可以访问 PCMCIA 设备的属性内存：

-   [访问属性的 PCMCIA 设备内存的要求](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/requirements-for-accessing-attribute-memory-of-a-pcmcia-device)

-   [通过使用插 I/O 请求访问 PCMCIA 属性内存](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-by-using-a-plug-and-play-i-o-request)

    这是一个简单的方法对于大多数情况下，已足够，但只能运行在 IRQL&lt;调度\_级别。

-   [通过使用总线访问 PCMCIA 属性内存\_接口\_标准接口](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-by-using-a-bus-interface-standard-inter)

    此方法消除了 I/O 请求的开销，并可以运行在 IRQL &lt;= 调度\_级别

-   [通过永久内存窗口访问 PCMCIA 属性内存](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-through-a-permanent-memory-window)

    驱动程序的 ISR 可以使用此方法直接在 IRQL DIRQL 运行时访问内存。

-   [通过使用 PCMCIA 访问 PCMCIA 属性内存\_接口\_标准接口](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-pcmcia-attribute-memory-by-using-a-pcmcia-interface-standard-in)

    内存卡驱动程序可以使用此方法，在 IRQL &lt;= 调度\_级别。

这些方法支持通过*pcmcia.sys*，在 Windows 2000 和更高版本操作系统总线 PCMCIA 系统驱动程序。

 

 





