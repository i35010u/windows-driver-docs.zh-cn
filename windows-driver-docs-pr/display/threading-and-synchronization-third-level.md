---
title: 线程和同步第三级别
description: 线程和同步第三级别
keywords:
- 线程 WDK 显示，第三级
- 同步 WDK 显示，第三级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91bc903f576f4b3c96e4e653631237e938b4673d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832719"
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

 

