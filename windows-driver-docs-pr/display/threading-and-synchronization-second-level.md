---
title: 线程和同步第二级别
description: 线程和同步第二级别
ms.assetid: 2b7c1eae-6527-469e-a2fa-74d2a1246bd3
keywords:
- 线程处理 WDK 显示，第二个级别
- 同步 WDK 显示，第二个级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb41f8c030b099bef4756c69d7e238c45d36dd3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354693"
---
# <a name="threading-and-synchronization-second-level"></a>线程和同步第二级别


线程处理和同步的第二个级别等同于[的第三个级别](threading-and-synchronization-third-level.md)，只不过不逐出视频内存来承载 CPU 内存。 换而言之，只有一个线程 （即，调用线程） 中显示微型端口驱动程序是 Windows 显示驱动程序模型 (WDDM) 保证，图形硬件处于空闲状态，且没有直接内存访问 (DMA) 缓冲区当前正在处理的该驱动程序或通过 GPU 计划程序。 在第二个级别下进行到显示微型端口驱动程序的以下调用：

**请注意**  以便进行第二个级别，某些调用**HardwareAccess**标志必须设置内**D3DDDI\_ESCAPEFLAGS**结构是的成员**DXGKARG\_转义**。 如果未设置此标志，则调用将失败。

 

-   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)

-   [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)

-   [*DxgkDdiDispatchIoRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)

-   [*DxgkDdiEscape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)

-   [*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)

-   [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendMonitorModes*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)

-   [*DxgkDdiSetPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)

-   [*DxgkDdiSetTimingsFromVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settimingsfromvidpn)

-   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))

-   [*DxgkDdiSetVidPnSourceVisibility*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)

-   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)

 

 





