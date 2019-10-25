---
title: 线程和同步第三级别
description: 线程和同步第三级别
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- 线程 WDK 显示，第三级
- 同步 WDK 显示，第三级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54eddac923f5bab1972a2977e9608bfcb7e5461a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829321"
---
# <a name="threading-and-synchronization-third-level"></a>线程和同步第三级别


Windows 显示驱动程序模型（WDDM）保证以下对显示微型端口驱动程序的调用在线程和同步的第三个级别下进行。 这可确保只有单个线程（即调用线程）在驱动程序内。 此外，图形硬件处于空闲状态，驱动程序当前未处理直接内存访问（DMA）缓冲区或通过 GPU 计划程序进行处理，并且视频内存已完全逐出主机 CPU 内存。

-   [*DxgkDdiAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)

-   [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)

-   [*DxgkDdiRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)

-   [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)

-   [*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)

-   [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)

-   [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)

-   [*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_unload)

 

 





