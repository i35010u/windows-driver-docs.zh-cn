---
title: Windows 2000 显示驱动程序模型 (XDDM) 设计指南
description: Windows 2000 显示驱动程序模型 (XDDM) 设计指南
ms.assetid: 24cb232b-e289-45c8-8d55-42614a4dfd54
keywords:
- 显示设备 WDK
- 显示驱动程序模型 WDK Windows 2000
- Windows 2000 显示器驱动程序型号 WDK
- 显示驱动程序 WDK，Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dba79865a9f365d30c5e844576e284d3ca155fc6
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734199"
---
# <a name="windows-2000-display-driver-model-xddm-design-guide"></a>Windows 2000 显示驱动程序模型 (XDDM) 设计指南


## <span id="ddk_windows_2000_display_driver_model_gg"></span><span id="DDK_WINDOWS_2000_DISPLAY_DRIVER_MODEL_GG"></span>


在 Windows Vista 上运行的显示适配器驱动程序可遵循以下两种模型之一： [Windows 显示器驱动程序模型 (WDDM) ](windows-vista-display-driver-model-design-guide.md) 或 windows 2000 显示器驱动程序模型 (XDDM) 。 遵循 Windows 显示器驱动程序模型 (WDDM) 的驱动程序只能在 Windows Vista 和更高版本上运行。 符合 XDDM 的驱动程序通过 Windows 7) 在 Windows 2000 上运行。

> [!NOTE]
> XDDM 和 VGA 驱动程序将不会在 Windows 8 及更高版本上编译或运行。 如果将显示硬件连接到 Windows 8 计算机，而该计算机上没有一个已认证为支持 WDDM 1.2 或更高版本的驱动程序，则系统默认为运行 Microsoft 基本显示驱动程序。 保留此文档是出于历史目的。

 

以下各节介绍了 Windows 2000 显示器驱动程序模型：

-   [显示（Windows 2000 模型）简介](introduction-to-display--windows-2000-model-.md)

-   [显示驱动程序（Windows 2000 模型）](display-drivers--windows-2000-model-.md)

-   [DirectDraw](directdraw.md)

-   [Direct3D DDI](direct3d.md)

-   [DirectX 视频加速](directx-video-acceleration.md)

-   [Windows 2000 显示驱动程序模型中的视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)

-   [Windows 显示驱动程序模型 (WDDM) 的实现提示和要求 ](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)

-   [GDI](gdi.md)

**注意**   Windows 2000 显示驱动程序模型的文档不再包括有关如何创建在 Microsoft Windows 98/Me 平台上运行的显示驱动程序的信息。 如果要为 Windows 98/Me 创建显示驱动程序，可以使用随 Windows Vista 一起发布的 WDK 文档。 你可以从 [Microsoft Connect 网站](/collaborate/connect-redirect)获取适用于 WINDOWS Vista RTM 的 WDK。

 

 

