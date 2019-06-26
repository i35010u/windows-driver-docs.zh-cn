---
title: 管理 PDEV
description: 管理 PDEV
ms.assetid: f7badbe8-b24f-438a-8937-95bb98de6310
keywords:
- PDEV WDK DirectDraw
- 绘制 WDK DirectDraw PDEV
- DirectDraw WDK Windows 2000 显示 PDEV
- 已禁用的 PDEV WDK DirectDraw
- 已启用的 PDEV WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdc36ae04d725a4d369c71710319bc8b818bfa6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370139"
---
# <a name="managing-pdevs"></a>管理 PDEV


## <span id="ddk_managing_pdevs_gg"></span><span id="DDK_MANAGING_PDEVS_GG"></span>


**本主题仅适用于 Windows 2000 和更高版本。**

显示驱动程序调用的线程数是依赖于在设备上的现有 PDEVs 数。 每个设备都有一个已启用 PDEV 每适配器输出的最大值和无限的数量的已禁用 PDEVs。 如果禁用或启用通过调用驱动程序的 PDEV [ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)函数。 如果显示驱动程序管理禁用和启用 PDEVs 混合，操作系统将允许一个线程可以同时同时允许多个线程调用已禁用 PDEVs 的驱动程序函数调用与启用了 PDEV 的驱动程序函数。 例如， [ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt) PDEV 正在销毁由另一个已禁用时启用 PDEV 上可能运行[ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface). 即使单个显示器驱动程序管理多个已启用的 PDEVs，（例如，在多个监视器方案中），操作系统将仍然只允许一个线程调用到驱动程序代码中使用任何这些已启用 PDEVs。

如果显示驱动程序必须管理任何全局资源和 PDEVs 之间共享的硬件状态，显示驱动程序还必须处理任何必要同步。 显示驱动程序映射到会话的空间，因此每个会话都有其自己的全局变量集。 因此，不必须使用的显示驱动程序的全局变量来保存如互斥体同步对象。 相反，设备扩展的微型端口驱动程序，它映射到全局空间中存储该互斥体未会话空间。 您可以初始化中视频的微型端口驱动程序的 mutex [ *HwVidInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_initialize)函数。 然后，在显示驱动程序[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)函数可以通过将自定义 IOCTL 发送到的微型端口驱动程序获取互斥体的指针。 属于不同会话的显示驱动程序线程将具有不同副本的指针，但所有这些副本将指向同一个 mutex 对象。

显示驱动程序不能直接调用获取和释放互斥体，以便显示驱动程序必须依赖于要执行这些任务的微型端口驱动程序的内核例程。 微型端口驱动程序可以实现的功能可获取并释放此斥锁，并显示驱动程序无法获取对该函数中相同的自定义 IOCTL，使用它来获取互斥体本身的指针的指针。

可以使用已禁用 PDEV 调用仅以下有限的数量的驱动程序函数：

-   [*DdMapMemory* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mapmemory) （适用于正在取消映射的内存）

-   [**DrvDisableDirectDraw**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledirectdraw)

-   [**D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) （适用于系统内存）

-   [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [*DdDestroySurface*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)

-   [*DdLock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)

-   [*DdUnlock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)

-   [*DestroyD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

-   [**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)

-   [**DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)

-   [**DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)

-   [**DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)

 

 





