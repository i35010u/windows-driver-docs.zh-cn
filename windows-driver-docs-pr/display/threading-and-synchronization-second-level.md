---
title: 线程和同步第二级别
description: 线程和同步第二级别
ms.assetid: 2b7c1eae-6527-469e-a2fa-74d2a1246bd3
keywords:
- 线程 WDK 显示，第二级
- 同步 WDK 显示，第二级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fbf1260d74e23b66fc624b225153c87630b34eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829323"
---
# <a name="threading-and-synchronization-second-level"></a>线程和同步第二级别


第二级别的线程和同步与[第三](threading-and-synchronization-third-level.md)个级别相同，只不过视频内存不会被逐出主机 CPU 内存。 换句话说，Windows 显示驱动程序模型（WDDM）保证只有单个线程（即调用线程）在显示微型端口驱动程序内，图形硬件处于空闲状态，并且当前不处理直接内存访问（DMA）缓冲区驱动程序，或通过 GPU 计划程序传递的。 以下对显示微型端口驱动程序的调用将在第二个级别下进行：

**请注意**   为了使某些调用在第二个级别下进行，必须在**D3DDDI\_ESCAPEFLAGS**结构中设置**HardwareAccess**标志，该结构是**DXGKARG\_转义**的成员。 如果未设置此标志，则调用将失败。

 

-   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)

-   [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)

-   [*DxgkDdiDispatchIoRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)

-   [*DxgkDdiEscape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)

-   [*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)

-   [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendMonitorModes*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)

-   [*DxgkDdiSetPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)

-   [*DxgkDdiSetTimingsFromVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)

-   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))

-   [*DxgkDdiSetVidPnSourceVisibility*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)

-   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)

 

 





