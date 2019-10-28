---
title: 锁定重排分配
description: 锁定重排分配
ms.assetid: c9be52d9-36b2-4a0f-9629-01b31293af38
keywords:
- swizzled 分配锁定 WDK 显示
- 锁定 swizzled 分配 WDK 显示
- unswizzled 分配 WDK 显示
- 内存段 WDK 显示，锁定 swizzled 分配
- 分配 swizzle 锁定 WDK 显示
- 逐出分配 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0089975bb28eead2e58131df202db298a093f654
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840599"
---
# <a name="locking-swizzled-allocations"></a>锁定重排分配


视频内存管理器提供对 swizzled 分配的直接 CPU 访问的特殊支持（即显示微型端口驱动程序的[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数在**标志**中设置**swizzled**标志[**DXGK\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构的成员）。

当视频内存管理器将 CPU 可访问的分配从内存段逐出为 swizzled 时，显示微型端口驱动程序必须始终以线性格式存储它们。 因此，此类分配在 swizzled 时不能被，它们必须始终为驱动程序的[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数 swizzled 或 unswizzled。

另一方面，如果从内存段逐出，则标记为 swizzled 的分配无需始终以线性格式存储。 对于此类分配，视频内存管理器跟踪这些分配的 swizzling 状态，只需要驱动程序的*DxgkDdiBuildPagingBuffer*函数在某些传输操作期间 unswizzle 分配。

用户模式显示驱动程序调用了 Microsoft Direct3D 运行时的[**pfnLockCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数后，视频内存管理器和显示微型端口驱动程序的行为取决于分配的状态：

1.  内存段中的分配

    视频内存管理器将尝试获取 CPU 口径以提供对分配的线性访问。 如果视频内存管理器无法获取口径，视频内存管理器会将分配逐出到系统内存（除非驱动程序设置 D3DDDICB 的**DonotEvict**成员[ **\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)结构）。 当视频内存管理器调用显示微型端口驱动程序的[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数来传输分配时，显示微型端口驱动程序应 unswizzle 分配。

2.  分配已收回（swizzled）或位于口径段

    在 CPU 可以访问之前，必须 unswizzled 分配。 因此，视频内存管理器首先尝试将分配页面到内存段。 在内存段中进行分配后，视频内存管理器和显示微型端口驱动程序的行为与数字1中的行为相同。

3.  分配已逐出（unswizzled）

    如果分配已 unswizzled 系统内存，视频内存管理器将返回现有的分配指针，而不进行进一步的处理。

    为了使 GPU 使用之前 unswizzled 的分配，在 GPU 使用之前，必须先对其进行 reswizzled。 因此，在表面故障中，视频内存管理器和显示微型端口驱动程序的行为方式如下：

    -   内存段中的分配（通过 CPU 口径动态 unswizzled）

        分配已采用 GPU 可处理的 swizzled 格式。 因此，视频内存管理器不需要进一步的处理。

    -   分配到系统内存（unswizzled）

        分配页面包含 unswizzled 数据，无法映射到孔径段。 因此，分配必须分页到内存段中。 当视频内存管理器将显示微型端口驱动程序的[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数调用到分配中的页时，视频内存管理器会请求显示的显示微型端口驱动程序 swizzle 分配。

**请注意**   通过 cpu 口径对 swizzled 分配进行 Cpu 访问后，仍可在用户模式显示驱动程序终止 CPU 访问之前将其逐出。 这种情况的处理方式为第2号。 逐出的执行方式类似于应用程序和用户模式显示驱动程序都不可见。
同时，不允许对 swizzled 分配执行非覆盖锁定（即，通过设置[**D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)）的**IgnoreSync**成员获取的锁。 在任何给定时间，只有 CPU 或 GPU 可以访问此类分配。

 

 

 





