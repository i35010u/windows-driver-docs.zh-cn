---
title: PCMCIA_INTERFACE_STANDARD 接口的功能
description: PCMCIA_INTERFACE_STANDARD 接口的功能
ms.assetid: 301b4165-4753-4d55-9760-17628174c043
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 689cc25b053bcc9e9c4adc5c2445a86e8b7570d8
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384809"
---
# <a name="functionality-of-the-pcmcia_interface_standard-interface"></a>PCMCIA \_ 接口 \_ 标准接口的功能





本部分介绍 \_ \_ pcmcia 总线驱动程序在 Windows 2000 和更高版本的操作系统中支持的 pcmcia 接口标准接口功能。 PCMCIA \_ 接口 \_ 标准接口提供一组可由 PCMCIA 驱动程序直接调用的例程。 这些接口例程支持以下操作：

-   修改 PCMCIA 总线驱动程序所映射的 "内存" 窗口的属性

-   设置设备的 *Vpp* (辅助电源) 级别

-   确定卡内存是否受写保护

有关 PCMCIA 接口标准接口提供的例程的详细 \_ 信息 \_ ，请参阅 [Pcmcia \_ 接口 \_ 标准接口内存卡例程](/windows-hardware/drivers/ddi/index)。

 

