---
title: 线程和同步第三级别
description: 线程和同步第三级别
ms.assetid: 780d37d9-40c6-4737-9042-473810868227
keywords:
- 线程 WDK 显示，第三级
- 同步 WDK 显示，第三级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41658f9fdfa42344089da4a9797806ba2dbfd293
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063762"
---
# <a name="threading-and-synchronization-third-level"></a>线程和同步第三级别


Windows 显示驱动程序模型 (WDDM) 确保以下对显示微型端口驱动程序的调用在线程和同步的第三个级别下进行。 这可确保只有单个线程 (即，调用线程) 在驱动程序内。 此外，图形硬件处于空闲状态， (DMA) 缓冲区当前正在由驱动程序处理或通过 GPU 计划程序进行处理，并且视频内存已完全逐出主机 CPU 内存。

-   [*DxgkDdiAddDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)

-   [*DxgkDdiQueryChildRelations*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)

-   [*DxgkDdiRemoveDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)

-   [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)

-   [*DxgkDdiRestartFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)

-   [*DxgkDdiSetPowerState*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)

-   [*DxgkDdiStartDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   [*DxgkDdiStopDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)

-   [*DxgkDdiUnload*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_unload)

 

