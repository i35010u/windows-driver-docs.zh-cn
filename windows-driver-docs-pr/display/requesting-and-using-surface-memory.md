---
title: 请求和使用图面内存
description: 请求和使用图面内存
ms.assetid: 7913acc6-ff30-4f2a-8389-37a79940ae8b
keywords:
- surface memory WDK 显示
- 列出了 WDK 显示的表面
- 资源对象表面内存 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85d6f6eee6e9b11d6b8bdf5c5634738e25f097c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825928"
---
# <a name="requesting-and-using-surface-memory"></a>请求和使用图面内存


## <span id="ddk_requesting_and_using_surface_memory_gg"></span><span id="DDK_REQUESTING_AND_USING_SURFACE_MEMORY_GG"></span>


当 Microsoft Direct3D 运行时需要创建一个图面列表时，用户模式显示驱动程序将接收对其[**CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数的调用。 Direct3D 运行时为用户模式显示驱动程序用于回调到运行时的图面列表指定资源句柄。 用户模式显示驱动程序创建一个资源对象以表示图面列表，为此对象生成一个唯一的句柄，并将该句柄返回到 Direct3D 运行时。 运行时在后续的驱动程序调用中使用这个唯一的句柄来标识图面列表。 运行时通过在[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**pSurfList**成员中包含的数组中指定图面的索引来标识特定图面。

由于用户模式显示驱动程序在引用资源的调用中接收驱动程序定义的资源句柄，因此，驱动程序不需要执行开销较高的句柄查找来查找驱动程序定义的资源对象。 同样，如果运行时也无需执行句柄查找，则用户模式显示驱动程序会在用户模式显示驱动程序调用运行时时使用 Direct3D 运行时定义的资源句柄。

用户模式显示驱动程序调用[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数为曲面分配内存。 在**pfnAllocateCb**调用中，用户模式显示驱动程序可以分别为[**D3DDDICB\_分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)和[**D3DDDI\_ALLOCATIONINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)结构的**pPrivateDriverData**成员中的图面列表和每个单独的图面传递专用数据。 但是，用户模式显示驱动程序无法接收来自**pPrivateDriverData**成员的私有数据。 用户模式显示驱动程序可以为此私有数据分配内存，并且可以在**pfnAllocateCb**调用返回后释放内存，也可以使用堆栈内存传递此私有数据。 **PfnAllocateCb**函数将向用户模式显示驱动程序返回每个分配的图面的每个分配的句柄。

**请注意**   用户模式显示驱动程序必须为每个设备的每个共享表面调用一次**pfnAllocateCb**函数。 例如，如果设备1创建一个同时由设备2、3和4使用的共享图面，则设备2、3和4还必须为共享表面调用**pfnAllocateCb**一次，以便检索分配句柄。

 

用户模式显示驱动程序必须为每个分配句柄跟踪每个图面，通常情况下，可通过维护 surface to 分配控点表。 用户模式显示驱动程序应将每个分配句柄存储在驱动程序定义的资源对象中。

当 Direct3D 运行时在先前分配的表面上执行操作（例如，在对用户模式显示驱动程序的[**Blt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)函数的调用中）时，用户模式显示驱动程序将接收资源的句柄，可能带有 surface 索引。 用户模式显示驱动程序使用此资源句柄检索驱动程序定义的资源对象。 驱动程序获取存储在资源对象中的分配句柄，并将它们汇编在命令缓冲区中。 用户模式显示驱动程序在调用[**pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)函数时使用对应于图面的分配句柄，将命令缓冲区提交给显示微型端口驱动程序。 显示微型端口驱动程序可以调用[**DxgkCbGetHandleData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_gethandledata)函数来确定用户模式显示驱动程序所引用的 surface 分配。

 

 





