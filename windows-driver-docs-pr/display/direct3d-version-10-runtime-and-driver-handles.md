---
title: Direct3D 版本 10 运行时和驱动程序句柄
description: Direct3D 版本 10 运行时和驱动程序句柄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9222fcfca024cabb50742cce454e71b2f6febf6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809425"
---
# <a name="direct3d-version-10-runtime-and-driver-handles"></a>Direct3D 版本 10 运行时和驱动程序句柄


Direct3D 版本10运行时和驱动程序句柄共享相同的生命周期。 Direct3D 运行时指定对 create 类型函数的调用之间的对象的生存期 (例如， [**CreateResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)) ，并调用销毁类型函数 (例如 [**DestroyResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)) 。 运行时提供驱动程序句柄值和运行时句柄值。 这些句柄本质上是用强类型进行包装以标识正在操作的对象的指针。 下面是资源的运行时和驱动程序句柄的示例：

```cpp
// Strongly typed handle to identify a resource object to the driver: 
typedef struct D3D10DDI_HRESOURCE
{
    void* pDrvPrivate; // Pointer to memory location as large as the driver requested.
} D3D10DDI_HRESOURCE;

// Strongly typed handle to identify a resource object to the runtime:
typedef struct D3D10DDI_HRTRESOURCE
{
    void* handle;
} D3D10DDI_HRTRESOURCE;
```

呈现设备对象及其子对象的所有驱动程序句柄都遵循以下两个通过的创建机制：

1.  为了确定驱动程序句柄指针的值，运行时首先调用 _CalcPrivate_**ObjType**_Size_ 函数 (例如， [**CalcPrivateResourceSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateresourcesize) 函数) 。 在此调用中，运行时会传入创建参数 (例如，指向 [**D3D10DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource) 结构的指针) 。 运行时还会传入对 _Create_**ObjType** 函数的调用中的创建参数。

    通常，在调用 _CalcPrivate_**ObjType**_大小_ 期间，用户模式显示驱动程序无需分配任何内容。 但是，如果驱动程序执行并失败或必须指示任何其他类型的故障情况，则驱动程序可以返回大小 \_ T (-1 ) 以阻止创建句柄。 然后，运行时将一个 E \_ OUTOFMEMORY 错误条件返回到调用应用程序。

    至少，驱动程序应从 **sizeof (** 对 \* _CalcPrivate_**ObjType**_大小_ 的调用返回 sizeof (void **)** 。

2.  如果运行时可以分配足够的空间来满足用户模式显示驱动程序所需的大小，则运行时将调用 _Create_**ObjType** 函数 (例如， [**CreateResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource) 具有相同创建参数的) 以及驱动程序句柄的新唯一值。 驱动程序句柄的指针值在句柄的整个生存期内都是唯一的并且是常量，因为它指向的内存区域的大小是由 _CalcPrivate_**ObjType**_size_ 返回的。 用户模式显示驱动程序可根据需要使用此内存区域。 驱动程序应通过将经常访问的数据定位到运行时提供的内存区域，提高效率。

 

