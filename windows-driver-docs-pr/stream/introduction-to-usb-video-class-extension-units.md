---
title: USB 视频类扩展单元简介
description: USB 视频类扩展单元简介
ms.assetid: a46feb97-771e-4efd-872e-4a4b0fb3b705
keywords:
- 扩展单元-WDK USB 视频类，关于扩展单元
- USB 视频类驱动程序 WDK AVStream，关于扩展单元
- 视频类驱动程序 WDK USB，扩展单元，关于
- UVC 驱动程序 WDK AVStream，扩展单元，关于
- 扩展单元-WDK USB 视频类，关于
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98986cb808a00ed380f715ae1d024d47798dae5c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190905"
---
# <a name="introduction-to-usb-video-class-extension-units"></a>USB 视频类扩展单元简介


*USB 视频类*规范定义了一种机制，用于扩展符合该规范的设备的功能，并描述了扩展单元的行为。 独立硬件供应商 (Ihv) 可以通过添加超出规范中所述功能的功能来增强其设备的价值。

此扩展机制需要操作系统支持和某些用户模式插件，以便应用程序可以使用这些扩展。 USB 视频类驱动程序体系结构提供了这样一种机制，以便 Ihv 可以将扩展设备功能作为 COM Api 公开。 本文档介绍创建和注册此类插件所需的步骤。

### <a name="sdk-information"></a>SDK 信息

Vidcap 中定义了 IKsTopologyInfo、ISelector 和 IKsNodeControl。

在 Windows Vista 和更高版本中，Vidcap 作为 Microsoft Windows SDK 的一部分包含。

Microsoft DirectShow 文档包含相应的参考页。 Ksmedia 中定义了全局唯一标识符 (GUID) 类型和与其他 USB 视频相关的常量。 有关详细信息，请参阅 [USB 视频类属性](usb-video-class-properties.md) 和 [内核流式处理拓扑节点](./kernel-streaming-topology-nodes.md)。

 

