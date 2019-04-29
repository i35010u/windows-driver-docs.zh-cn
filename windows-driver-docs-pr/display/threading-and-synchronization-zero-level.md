---
title: 线程和同步零级别
description: 线程和同步零级别
ms.assetid: 2baf91e8-fafb-40e2-a24c-cbf04fe45274
keywords:
- 线程处理 WDK 显示，零级别
- 同步 WDK 显示，零级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf129424c33ab2073cc23cf1babe220e4e15167e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389826"
---
# <a name="threading-and-synchronization-zero-level"></a>线程和同步零级别


Windows 显示驱动程序模型 (WDDM) 允许到显示微型端口驱动程序的以下调用以可重入的方式进行。 也就是说，多个线程可以同时输入驱动程序通过调用以下函数：

**请注意**  尽管两个或多个线程可以在驱动程序运行在同一时间，没有两个线程可以属于单个进程。

 

-   [*DxgkDdiCloseAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559592)

-   [*DxgkDdiCollectDbgInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559595)
    **注意**  [*DxgkDdiCollectDbgInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559595)应收集各种的调试信息故障和可以在任何时间和高 IRQL 调用 (即，IRQL， *DxgkDdiCollectDbgInfo*通常在运行未定义)。 在任何情况下， *DxgkDdiCollectDbgInfo*必须验证所需的调试信息和正确的同步的可用性。 但是，如果**原因**的成员[ **DXGKARG\_COLLECTDBGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff557545)结构*pCollectDbgInfo*参数*DxgkDdiCollectDbgInfo*点设置为[视频\_TDR\_超时\_检测到](https://msdn.microsoft.com/library/windows/hardware/hh994433)或[视频\_引擎\_超时\_已检测](https://msdn.microsoft.com/library/windows/hardware/hh994433)，该驱动程序必须确保*DxgkDdiCollectDbgInfo*是可分页，运行在 IRQL =**被动\_级别**，并支持同步零级别。

     

-   [*DxgkDdiControlEtwLogging*](https://msdn.microsoft.com/library/windows/hardware/ff559599)

-   [*DxgkDdiCreateAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559606)

-   [*DxgkDdiCreateContext*](https://msdn.microsoft.com/library/windows/hardware/ff559612)

-   [*DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)

-   [*DxgkDdiDescribeAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559620)

-   [*DxgkDdiDestroyAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559630)

-   [*DxgkDdiDestroyContext*](https://msdn.microsoft.com/library/windows/hardware/ff559636)

-   [*DxgkDdiDestroyDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559639)

-   [*DxgkDdiDpcRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559645)

-   [*DxgkDdiEnumVidPnCofuncModality*](https://msdn.microsoft.com/library/windows/hardware/ff559649)

-   [*DxgkDdiGetScanLine*](https://msdn.microsoft.com/library/windows/hardware/ff559668)

-   [*DxgkDdiGetStandardAllocationDriverData*](https://msdn.microsoft.com/library/windows/hardware/ff559673)

-   [*DxgkDdiInterruptRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559680)

-   [*DxgkDdiIsSupportedVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559684)

-   [*DxgkDdiMiracastCreateContext*](https://msdn.microsoft.com/library/windows/hardware/dn323748)

-   [*DxgkDdiMiracastDestroyContext*](https://msdn.microsoft.com/library/windows/hardware/dn323749)

-   [*DxgkDdiMiracastIoControl*](https://msdn.microsoft.com/library/windows/hardware/dn323750)

-   [*DxgkDdiMiracastQueryCaps*](https://msdn.microsoft.com/library/windows/hardware/dn323751)

-   [*DxgkDdiOpenAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559699)

-   [*DxgkDdiPresent*](https://msdn.microsoft.com/library/windows/hardware/ff559743)

-   [*DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)

-   [*DxgkDdiQueryCurrentFence*](https://msdn.microsoft.com/library/windows/hardware/ff559758)

-   [*DxgkDdiRecommendFunctionalVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559775)

-   [*DxgkDdiRecommendVidPnTopology*](https://msdn.microsoft.com/library/windows/hardware/ff559782)

-   [*DxgkDdiRender*](https://msdn.microsoft.com/library/windows/hardware/ff559793)

-   [*DxgkDdiRenderKm*](https://msdn.microsoft.com/library/windows/hardware/ff559800)

-   [*DxgkDdiResetDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559808)

 

 





