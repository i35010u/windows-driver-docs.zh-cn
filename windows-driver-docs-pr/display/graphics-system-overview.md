---
title: 图形系统概述
description: 图形系统概述
keywords:
- GDI WDK Windows 2000 显示，关于图形系统
- 图形驱动程序 WDK Windows 2000 显示，关于图形系统
- 绘制 WDK GDI，关于图形系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00cb93b7d489c8cb23de9cdc8a0f937b80970366
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827297"
---
# <a name="graphics-system-overview"></a>图形系统概述


## <span id="ddk_graphics_system_overview_gg"></span><span id="DDK_GRAPHICS_SYSTEM_OVERVIEW_GG"></span>


Microsoft Windows NT (TM) 操作系统提供了一个强大的图形体系结构，在该体系结构中，第三方图形硬件公司可以轻松地将其视频显示和打印设备相集成。 以下各节提供了编写有效图形驱动程序的设计准则：

-   [**图形 DDI**](using-the-graphics-ddi.md)

    本部分介绍 Windows 图形设备接口 (GDI) 和图形设备驱动程序接口 (DDI) 。 讨论了显示和打印驱动程序所共有的设计和实现详细信息。

-   [**Windows 显示驱动程序模型 (WDDM) 设计指南**](windows-vista-display-driver-model-design-guide.md)

    [**Windows 2000 显示驱动程序模型 (XDDM) 设计指南**](windows-2000-display-driver-model-design-guide.md)

    以下部分介绍基于 Windows NTâˆ的操作系统中的视频显示环境，并提供显示、视频微型端口和监视驱动程序编写器的设计和实现详细信息。 请注意，不能在 Windows 8 和更高版本的计算机上安装符合 Windows 2000 显示驱动程序模型的驱动程序。

-   [**打印设备设计指南**](../print/index.md)

    本部分介绍在基于 Windows NTâˆ的操作系统中构成打印环境的驱动程序和打印后台处理程序。 Windows 驱动程序工具包的此部分中的部分 (WDK) 指定如何提供自定义的驱动程序和后台处理程序组件，以便支持新的打印机硬件和网络配置。

 

