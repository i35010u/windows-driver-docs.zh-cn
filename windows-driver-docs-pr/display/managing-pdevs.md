---
title: 管理 PDEV
description: 管理 PDEV
keywords:
- PDEV WDK DirectDraw
- 绘制 WDK DirectDraw，PDEV
- DirectDraw WDK Windows 2000 显示，PDEV
- 禁用的 PDEV WDK DirectDraw
- 已启用 PDEV WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f1936829e15da34e8f81db2cef915916be9e879
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793897"
---
# <a name="managing-pdevs"></a>管理 PDEV


## <span id="ddk_managing_pdevs_gg"></span><span id="DDK_MANAGING_PDEVS_GG"></span>


**本主题仅适用于 Windows 2000 和更高版本。**

调入显示驱动程序的线程数取决于设备上现有 PDEVs 的数目。 每个设备的每个适配器输出最多具有一个已启用的 PDEV，而禁用的 PDEVs 数最多为个。 通过调用驱动程序的 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode) 函数，禁用或启用了 PDEV。 当显示驱动程序管理已禁用和已启用的 PDEVs 组合时，操作系统允许单个线程调用具有已启用的 PDEV 的驱动程序函数，同时允许多个线程调用具有已禁用 PDEVs 的驱动程序函数。 例如， [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt) 可以在已启用的 PDEV 上运行，而另一个禁用的 PDEV 被 [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface)销毁。 即使单个显示驱动程序管理多个已启用的 PDEVs， (例如，在多监视器方案) 中，操作系统仍然只允许单个线程使用任何启用的 PDEVs 调用驱动程序代码。

如果显示驱动程序必须管理 PDEVs 之间共享的任何全局资源和硬件状态，则显示驱动程序还必须处理任何必要的同步。 显示驱动程序映射到会话空间，因此每个会话都有自己的全局变量集。 因此，您不能使用显示驱动程序全局变量来保存同步对象，例如互斥体。 相反，请将互斥体存储在视频微型端口驱动程序的设备扩展中，该驱动程序映射到全局空间而非会话空间。 可以在视频微型端口驱动程序的 [*HwVidInitialize*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize) 函数中初始化互斥体。 然后，显示驱动程序的 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数可以通过将自定义 IOCTL 发送到视频微型端口驱动程序来获取指向互斥体的指针。 显示属于不同会话的驱动程序线程将具有不同的指针副本，但所有这些副本将指向相同的 mutex 对象。

不允许显示驱动程序直接调用获取和释放互斥体的内核例程，因此显示驱动程序必须依赖视频微型端口驱动程序来执行这些任务。 视频微型端口驱动程序可以实现一个函数，该函数可获取和释放互斥体，而显示驱动程序可以获取指向此函数的指针，该指针用于获取指向互斥体本身的指针。

对于已禁用的 PDEV，只能调用以下有限数量的驱动程序函数：

-   [*DdMapMemory*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mapmemory) (仅用于取消映射内存) 

-   [**DrvDisableDirectDraw**](/windows/win32/api/winddi/nf-winddi-drvdisabledirectdraw)

-   仅限系统内存的 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) () 

-   [**D3dDestroyDDLocal**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [**D3dContextCreate**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)

-   [*DdLock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)

-   [*DdUnlock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)

-   [*DestroyD3DBuffer*](/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

-   [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode)

-   [**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev)

-   [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface)

-   [**DrvResetPDEV**](/windows/win32/api/winddi/nf-winddi-drvresetpdev)

 

