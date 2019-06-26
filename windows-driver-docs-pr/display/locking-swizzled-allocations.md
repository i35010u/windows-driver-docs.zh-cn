---
title: 锁定重排分配
description: 锁定重排分配
ms.assetid: c9be52d9-36b2-4a0f-9629-01b31293af38
keywords:
- 锁定 WDK 显示 swizzled 分配
- 锁定显示 WDK swizzled 分配
- 孔径取消调配分配 WDK 显示
- 锁定 swizzled 分配的内存段 WDK 显示
- 分配 swizzle 锁 WDK 显示
- 逐出的分配 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 114256e7cc9f1e6e79ca5b39e45967156f467dcf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360889"
---
# <a name="locking-swizzled-allocations"></a>锁定重排分配


视频内存管理器提供特殊支持直接 swizzled 分配 CPU 访问 (也就是说，在其中分配显示微型端口驱动程序[ **DxgkDdiCreateAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)函数集**Swizzled**中的标志**标志**的成员[ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)结构)。

当视频内存管理器逐出未标记的驱动程序，因为 swizzled 内存段中的可访问 CPU 的分配时，显示微型端口驱动程序必须始终将其存储在以线性格式。 因此，此类分配不能为 swizzled 它们位于 aperture 段，而它们必须始终为 swizzled 或驱动程序的 unswizzled [ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数。

但是，标记为 swizzled 的分配不需要始终存储在以线性格式时从内存段中逐出。 对于此类分配的视频内存管理器跟踪 swizzling 状态的那些分配，并仅需要的驱动程序*DxgkDdiBuildPagingBuffer* unswizzle 某些传输操作期间的分配函数。

用户模式下显示后，驱动程序将调用 Microsoft Direct3D 运行时[ **pfnLockCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数、 视频内存管理器和显示微型端口驱动程序行为，具体取决于以下的方式分配的状态：

1.  分配的内存段中

    视频内存管理器尝试获取 CPU aperture，以提供对分配的线性访问。 视频内存管理器的视频内存管理器无法获取 aperture，如果逐出回系统内存分配 (除非驱动程序设置**DonotEvict**的成员[ **D3DDDICB\_LOCKFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)结构)。 当视频内存管理器调用显示微型端口驱动程序[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数传输分配，显示微型端口驱动程序应 unswizzle 分配。

2.  分配逐出 (swizzled) 或位于 aperture 段

    分配必须先孔径取消调配 CPU 都可以访问它。 因此，视频内存管理器首先尝试分配到一个内存段中页上。 分配位于一个内存段后，视频内存管理器和显示微型端口驱动程序的行为如编号 1 中所示。

3.  逐出的分配 （孔径取消调配）

    如果分配已孔径取消调配到系统内存，视频内存管理器返回现有分配指针而不会进一步处理。

    为了使 GPU 使用以前孔径取消调配的分配，分配必须先 reswizzled GPU 使用它。 因此，图面上出现错误，视频内存管理器和显示微型端口驱动程序的行为在以下方面：

    -   内存段 （由 CPU aperture 动态孔径取消调配） 中的分配

        分配已在 GPU 可以处理的 swizzled 格式。 因此，无需进一步处理需要的视频内存管理器。

    -   分配到系统内存 （孔径取消调配） 中逐出

        分配的页则包含孔径取消调配数据，不能映射到 aperture 段。 因此，必须在一个内存段中分页分配。 当视频内存管理器调用显示微型端口驱动程序[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数中分配的视频内存管理器页请求显示微型端口驱动程序swizzle 分配。

**请注意**   swizzled 分配下通过 CPU aperture CPU 访问后，它可以仍被逐出之前用户模式显示驱动程序终止的 CPU 访问权限。 这种情况下处理如数字 2 所示。 逐出，就可以使用对应用程序和用户模式显示驱动程序不可见的方式执行。
此外，no-overwrite 锁 (即，通过设置获得的锁**IgnoreSync**的成员[ **D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)) 上 swizzled 不允许分配。 仅 CPU 还是 GPU 可以访问此类在任何给定时间分配。

 

 

 





