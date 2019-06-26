---
title: 请求和使用图面内存
description: 请求和使用图面内存
ms.assetid: 7913acc6-ff30-4f2a-8389-37a79940ae8b
keywords:
- 图面上的内存 WDK 显示
- 列出 WDK 显示的图面
- 资源对象图面上内存 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37d574d5e4cb5789751a02bb3407c69807553fe4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356354"
---
# <a name="requesting-and-using-surface-memory"></a>请求和使用图面内存


## <span id="ddk_requesting_and_using_surface_memory_gg"></span><span id="DDK_REQUESTING_AND_USING_SURFACE_MEMORY_GG"></span>


用户模式显示驱动程序接收到调用其[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)时需要的图面列表创建一个 Microsoft Direct3D 运行时的功能。 Direct3D 运行时指定的资源句柄的图面，用户模式显示驱动程序用来回调到运行时列表。 用户模式显示驱动程序创建的资源对象来表示应用层协议的列表，生成此对象的唯一句柄并返回到 Direct3D 运行时返回的句柄。 运行时使用此唯一的句柄在后续的驱动程序调用中标识的图面列表。 运行时通过指定中包含的数组中的图面的索引来标识特定的面**pSurfList**的成员[ **D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构。

因为用户模式显示驱动程序，请参阅资源的调用中接收的驱动程序定义的资源句柄，该驱动程序不需要执行成本高昂的句柄查找以查找驱动程序定义的资源对象。 同样，以便在运行时也不需要执行句柄查找，用户模式驱动程序使用 Direct3D 的运行时定义的资源句柄时显示用户模式显示驱动程序返回到运行时调用。

用户模式显示驱动程序调用[ **pfnAllocateCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数分配内存来存放图面。 在中**pfnAllocateCb**调用中，用户模式显示驱动程序可以将传递私有数据的图面列表和在每个单个面**pPrivateDriverData**的成员[ **D3DDDICB\_分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)并[ **D3DDDI\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)结构，分别。 但是，用户模式显示驱动程序不能接收从专用数据**pPrivateDriverData**成员。 用户模式显示驱动程序可以为此专用数据分配内存并可以释放内存后的**pfnAllocateCb**调用返回时，也可以使用堆栈内存传递此专用数据。 **PfnAllocateCb**函数返回到用户模式显示驱动程序的每个已分配的图面每个分配的句柄。

**请注意**  用户模式显示驱动程序必须调用**pfnAllocateCb**函数一次为每个设备每个共享图面。 例如，如果设备 1 创建 2、 3 和 4 的设备也使用共享图面，然后设备 2、 3 和 4 还必须调用**pfnAllocateCb**一次针对共享表面，以检索分配句柄。

 

用户模式显示驱动程序必须跟踪每个面对每个分配句柄，通常情况下，通过维护面分配句柄表。 用户模式显示驱动程序应存储在驱动程序定义的资源对象中每个分配句柄。

当 Direct3D 运行时执行以前分配的图面上的操作 (例如，对用户模式下的调用中显示器驱动程序的[ **Blt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)函数)，用户模式显示驱动程序将收到句柄的资源，也可能包含一个图面上的索引。 用户模式显示驱动程序使用此资源句柄来检索驱动程序定义的资源对象。 该驱动程序获取的资源对象中存储的分配句柄，并将它们汇编命令缓冲区中。 用户模式显示驱动程序将使用对应于表面时调用的分配句柄[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)函数以提交到显示微型端口驱动程序的命令缓冲区。 显示微型端口驱动程序可以调用[ **DxgkCbGetHandleData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_gethandledata)函数来确定哪些图面上分配引用用户模式显示驱动程序。

 

 





