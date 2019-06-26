---
title: 线程和同步第三级别
description: 线程和同步第三级别
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- 线程处理 WDK 显示，第三个级别
- 同步 WDK 显示、 第三个级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a5c71dcc40e28daa3dcee3db284f16beb506309
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354691"
---
# <a name="threading-and-synchronization-third-level"></a>线程和同步第三级别


Windows 显示驱动程序模型 (WDDM) 保证的线程处理和同步的第三个级别下执行到显示微型端口驱动程序的以下调用。 这可确保只有一个线程 （即，调用线程） 是在驱动程序中。 此外，图形硬件是空闲状态，不直接内存访问 (DMA) 缓冲区当前处理由驱动程序或通过 GPU 计划程序，并且完全逐出的视频内存来承载 CPU 内存。

-   [*DxgkDdiAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_add_device)

-   [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)

-   [*DxgkDdiRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_remove_device)

-   [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)

-   [*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)

-   [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_set_power_state)

-   [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_stop_device)

-   [*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_unload)

 

 





