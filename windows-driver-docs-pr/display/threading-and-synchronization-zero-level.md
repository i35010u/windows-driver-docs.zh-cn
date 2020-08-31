---
title: 线程和同步零级别
description: 线程和同步零级别
ms.assetid: 2baf91e8-fafb-40e2-a24c-cbf04fe45274
keywords:
- 线程 WDK 显示，零级
- 同步 WDK 显示，零级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffcca147478dcfe696bab934eb3f5f15e72fb132
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063752"
---
# <a name="threading-and-synchronization-zero-level"></a>线程和同步零级别


Windows 显示驱动程序模型 (WDDM) 允许以可重入方式进行以下对显示微型端口驱动程序的调用。 也就是说，多个线程可以通过调用以下函数同时进入驱动程序：

**注意**   尽管两个或多个线程可以同时在驱动程序中运行，但不能有两个线程属于单个进程。

 

-   [*DxgkDdiCloseAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_closeallocation)

-   [*DxgkDdiCollectDbgInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo) 
    **请注意**，  [*DxgkDdiCollectDbgInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)应收集各种故障的调试信息，并且可随时调用，在高 IRQL (上， *DxgkDdiCollectDbgInfo*运行时的 irql 通常不确定) 。 在任何情况下， *DxgkDdiCollectDbgInfo* 必须验证所需的调试信息的可用性和正确的同步。 但是，如果[**DXGKARG \_ COLLECTDBGINFO**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_collectdbginfo)结构的*pCollectDbgInfo*参数设置**Reason**为 "[检测到视频 \_ TDR \_ 超时 \_ ](../debugger/bug-check-code-reference2.md) " 或[检测到视频 \_ 引擎 \_ 超时 \_ ](../debugger/bug-check-code-reference2.md)，则驱动程序必须确保*DxgkDdiCollectDbgInfo*可分页，以 IRQL =**被动 \_ 级别**运行，并支持同步零级别。 *DxgkDdiCollectDbgInfo*

     

-   [*DxgkDdiControlEtwLogging*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_control_etw_logging)

-   [*DxgkDdiCreateAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)

-   [*DxgkDdiCreateContext*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)

-   [*DxgkDdiCreateDevice*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)

-   [*DxgkDdiDescribeAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_describeallocation)

-   [*DxgkDdiDestroyAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyallocation)

-   [*DxgkDdiDestroyContext*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroycontext)

-   [*DxgkDdiDestroyDevice*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroydevice)

-   [*DxgkDdiDpcRoutine*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)

-   [*DxgkDdiEnumVidPnCofuncModality*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)

-   [*DxgkDdiGetScanLine*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)

-   [*DxgkDdiGetStandardAllocationDriverData*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)

-   [*DxgkDdiInterruptRoutine*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)

-   [*DxgkDdiIsSupportedVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)

-   [*DxgkDdiMiracastCreateContext*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)

-   [*DxgkDdiMiracastDestroyContext*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)

-   [*DxgkDdiMiracastIoControl*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)

-   [*DxgkDdiMiracastQueryCaps*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps)

-   [*DxgkDdiOpenAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_openallocationinfo)

-   [*DxgkDdiPresent*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)

-   [*DxgkDdiQueryAdapterInfo*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)

-   [*DxgkDdiQueryCurrentFence*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querycurrentfence)

-   [*DxgkDdiRecommendFunctionalVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)

-   [*DxgkDdiRecommendVidPnTopology*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)

-   [*DxgkDdiRender*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)

-   [*DxgkDdiRenderKm*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)

-   [*DxgkDdiResetDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_reset_device)

 

