---
title: 迁移到 Windows 显示驱动程序模型 (WDDM)
description: 迁移到 Windows 显示驱动程序模型 (WDDM)
ms.assetid: 7f926aa7-1698-4a4e-a1ce-54a316bdc0cd
keywords:
- 显示驱动程序模型 WDK Windows Vista 迁移
- Windows Vista 显示器驱动程序模型 WDK，迁移
- 迁移显示器驱动程序模型 WDK Windows Vista
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61e17f6a2b21b788cb515780879d5c1622c29930
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390826"
---
# <a name="migrating-to-the-windows-display-driver-model-wddm"></a>迁移到 Windows 显示驱动程序模型 (WDDM)


## <span id="ddk_migrating_to_the_longhorn_display_driver_model_gg"></span><span id="DDK_MIGRATING_TO_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


迁移到 Windows 显示驱动程序模型 (WDDM)） 要求驱动程序编写器编写完全不同的显示和视频的微型端口驱动程序。 类似于[Windows 2000 显示器驱动程序模型 (XDDM)](windows-2000-display-driver-model-design-guide.md)，需要配对 WDDM 显示器驱动程序，并显示微型端口驱动程序。 但是，在 WDDM 显示器驱动程序运行在用户模式下。 此外，该模型不使用 Windows 图形设备接口 (GDI) 引擎; 的服务该模型使用 Microsoft Direct3D 运行时和 Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 的服务。

WDDM 支持显示和编写根据 XDDM 的微型端口驱动程序。 但是，新的驱动程序应编写为 WDDM 驱动程序，只要有可能，若要充分利用从 Windows Vista 开始提供的软件和硬件功能。

尽管驱动程序编写人员可以重复使用其 WDDM 驱动程序中的低级别依赖于硬件的代码，但它们应重新编写新的设备驱动程序接口 (DDI) 的相关代码。 在编写 WDDMdrivers 时，请考虑以下几点：

-   显示微型端口驱动程序必须实现一修改后的入口点函数与操作系统和 DirectX 图形内核子系统进行交互。 有关详细信息，请参阅[ **DriverEntry 的显示微型端口驱动程序**](https://msdn.microsoft.com/library/windows/hardware/ff556157)。 显示微型端口驱动程序可以调用任何有案可稽的内核函数。

-   显示微型端口驱动程序动态加载适当的 DirectX 图形内核子系统。 显示微型端口驱动程序和 DirectX 图形内核子系统相互通过接口调用。

-   显示微型端口驱动程序不再需要处理最多有视频 I/O 控制代码 (IOCTL)。 在 XDDM，内核模式显示驱动程序使用这些代码与微型端口驱动程序进行通信。 WDDM，在用户模式显示驱动程序进行通信与 Direct3D 运行时;WDDM 图形内核子系统，反过来，与显示微型端口驱动程序进行通信。
    **请注意**   WDDM，仍用于以下 Ioctl 和显示微型端口驱动程序必须处理它们：[**IOCTL\_视频\_查询\_颜色\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff567817)
    [**IOCTL\_视频\_句柄\_VIDEOPARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567805)

     

<!-- -->

-   用户模式显示驱动程序必须实现和导出[ **OpenAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff568601)函数，这将打开图形适配器的实例。 用户模式显示驱动程序还必须实现[ **CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540634)函数，创建处理的呈现状态集合的显示设备的表示形式。

-   用户模式显示驱动程序[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)函数，以及显示微型端口驱动程序[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)函数中，替换[ *DdCanCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549213)， [ *DdCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549263)，和[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840) XDDM 中的函数。

-   大多数剩余用户模式显示驱动程序函数实现的相同的 XDDM 的内核模式显示驱动程序实现以下功能：
    -   [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数和[ **DP2** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)操作代码
    -   [动作补偿回调函数](https://msdn.microsoft.com/library/windows/hardware/ff568441)和[DirectX 视频加速结构](https://msdn.microsoft.com/library/windows/hardware/ff553882)

 

 





