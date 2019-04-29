---
title: Windows 2000 显示驱动程序模型 (XDDM) 设计指南
description: Windows 2000 显示驱动程序模型 (XDDM) 设计指南
ms.assetid: 24cb232b-e289-45c8-8d55-42614a4dfd54
keywords:
- 显示设备 WDK
- 显示器驱动程序模型 WDK Windows 2000
- Windows 2000 显示器驱动程序模型 WDK
- 显示驱动程序 WDK，Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9215569fd9aedb45b36a8246a7c21f89d1cd8b72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391132"
---
# <a name="windows-2000-display-driver-model-xddm-design-guide"></a>Windows 2000 显示驱动程序模型 (XDDM) 设计指南


## <span id="ddk_windows_2000_display_driver_model_gg"></span><span id="DDK_WINDOWS_2000_DISPLAY_DRIVER_MODEL_GG"></span>


显示适配器驱动程序在 Windows Vista 上运行，可以遵循两个模型之一： [Windows 显示驱动程序模型 (WDDM)](windows-vista-display-driver-model-design-guide.md)或 Windows 2000 显示器驱动程序模型 (XDDM)。 遵循到 Windows 显示器驱动程序模型 (WDDM) 驱动程序运行仅在 Windows Vista 和更高版本。 遵守 XDDM Windows 2000 和更高版本的操作系统 （包括 Windows Vista 和 Windows 7） 上运行的驱动程序。

**请注意**  XDDM 和 VGA 驱动程序不会在 Windows 8 和更高版本上进行编译。 如果显示硬件附加到没有认证支持 WDDM 1.2 或更高版本的驱动程序的 Windows 8 计算机，则系统会默认到正在运行的 Microsoft 基本显示驱动程序。

 

以下部分介绍了 Windows 2000 显示器驱动程序模型：

-   [显示 （Windows 2000 模式） 的简介](introduction-to-display--windows-2000-model-.md)

-   [显示驱动程序 （Windows 2000 模式）](display-drivers--windows-2000-model-.md)

-   [DirectDraw](directdraw.md)

-   [Direct3D DDI](direct3d.md)

-   [DirectX 视频加速](directx-video-acceleration.md)

-   [在 Windows 2000 显示器驱动程序模型中的视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)

-   [实现技巧和 Windows 显示器驱动程序模型 (WDDM) 的要求](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)

-   [GDI](gdi.md)

**请注意**   Windows 2000 显示器驱动程序模型的文档不再包含有关如何创建在 Microsoft Windows 98 运行的显示驱动程序的信息 / 我的平台。 如果你想要创建 Windows 98 的显示驱动程序 / 我来说，您可以使用发布的 WDK 文档与 Windows Vista。 你可以获取 WDK 为 Windows Vista RTM 从[Microsoft Connect 网站](https://go.microsoft.com/fwlink/p/?linkid=101629)。

 

 

 





