---
title: USB 视频类扩展单元简介
description: USB 视频类扩展单元简介
ms.assetid: a46feb97-771e-4efd-872e-4a4b0fb3b705
keywords:
- 有关扩展单位的扩展单位 WDK USB 视频类，
- 有关扩展单位 USB 视频类驱动程序 WDK AVStream
- 视频类有关驱动程序 WDK USB、 扩展单元
- UVC 驱动程序 WDK AVStream，扩展单位有关
- 扩展单位 WDK USB 视频类关于
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1005fec76ae91e9ced9a876c2d8321f0821f553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371128"
---
# <a name="introduction-to-usb-video-class-extension-units"></a>USB 视频类扩展单元简介


*USB 视频类*规范定义了一种机制来扩展功能的设备，以及符合该规范的扩展单位的行为。 独立硬件供应商 (Ihv) 可以增强其设备的值加上出现的功能规范中所述的更高版本。

此扩展机制需要操作系统支持和某些用户模式下插件，使应用程序可以使用这些扩展。 USB 视频类驱动程序体系结构提供这种机制，以便 Ihv 可以公开为 COM Api 扩展的设备功能。 本文档介绍创建和注册这种插件所需的步骤。

### <a name="sdk-information"></a>SDK 的信息

IKsTopologyInfo、 ISelector 和 IKsNodeControl Vidcap.h 中定义。

在 Windows Vista 和更高版本，Vidcap.h 是作为 Microsoft Windows SDK 的一部分。

Microsoft DirectShow 文档包含相应的参考页。 全局唯一标识符 (GUID) 类型和一些其他 USB 视频相关常量 Ksmedia.h 中定义。 有关详细信息，请参阅[USB 视频类属性](usb-video-class-properties.md)并[内核流式处理拓扑节点](https://msdn.microsoft.com/library/windows/hardware/ff560886)。

 

 




