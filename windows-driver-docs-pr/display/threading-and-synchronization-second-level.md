---
title: 线程和同步第二级别
description: 线程和同步第二级别
ms.assetid: 2b7c1eae-6527-469e-a2fa-74d2a1246bd3
keywords:
- 线程 WDK 显示，第二级
- 同步 WDK 显示，第二级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3c7c453ee71f3374beb12245300333b09f9cf0
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063764"
---
# <a name="threading-and-synchronization-second-level"></a>线程和同步第二级别


第二级别的线程和同步与 [第三](threading-and-synchronization-third-level.md)个级别相同，只不过视频内存不会被逐出主机 CPU 内存。 换句话说，Windows 显示驱动程序模型 (WDDM) 确保只有单个线程 (也就是说，调用线程) 在显示微型端口驱动程序内，图形硬件处于空闲状态，并且没有直接内存访问 (DMA) 当前正在由驱动程序处理或通过 GPU 计划程序进行处理。 以下对显示微型端口驱动程序的调用将在第二个级别下进行：

**注意**   为了使某些调用在第二个级别下进行，必须在作为**DXGKARG \_ ESCAPE**成员的**D3DDDI \_ ESCAPEFLAGS**结构中设置**HardwareAccess**标志。 如果未设置此标志，则调用将失败。

 

-   [*DxgkDdiCommitVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)

-   [*DxgkDdiControlInterrupt*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)

-   [*DxgkDdiDispatchIoRequest*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)

-   [*DxgkDdiEscape*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)

-   [*DxgkDdiNotifyAcpiEvent*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)

-   [*DxgkDdiQueryInterface*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)

-   [*DxgkDdiRecommendFunctionalVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendMonitorModes*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)

-   [*DxgkDdiSetPalette*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)

-   [*DxgkDdiSetTimingsFromVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)

-   [*DxgkDdiSetVidPnSourceAddress*](/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))

-   [*DxgkDdiSetVidPnSourceVisibility*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)

-   [*DxgkDdiUpdateActiveVidPnPresentPath*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)

 

