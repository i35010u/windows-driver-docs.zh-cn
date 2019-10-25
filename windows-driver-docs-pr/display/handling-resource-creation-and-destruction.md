---
title: 处理资源创建和销毁
description: 处理资源创建和销毁
ms.assetid: d443bdc3-1c5a-4372-9e6a-b8a4d21499b9
keywords:
- 资源创建 WDK 显示
- 资源销毁 WDK 显示
- 销毁资源 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd8df9e3466305c02a0a9a94055b3299f3983eb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838902"
---
# <a name="handling-resource-creation-and-destruction"></a>处理资源创建和销毁


若要使 Microsoft DirectX 图形内核子系统能够正确跟踪资源生存期并在操作系统中阻止内存泄漏，用户模式显示驱动程序必须正确创建和销毁资源。

Microsoft Direct3D 运行时调用以下用户模式显示驱动程序函数来创建用户模式资源。

-   [**CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)创建新的共享或非共享资源。

-   [**OpenResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)打开现有共享资源的视图。

在这两次调用中，Direct3D 运行时传递唯一的*用户模式运行时资源句柄*，用户模式显示驱动程序使用该句柄回调到运行时。 当*CreateResource*或*OpenResource*成功返回时，用户模式显示驱动程序将返回表示资源的唯一用户模式句柄。 此句柄是*用户模式驱动程序资源句柄*。 运行时在后续的驱动程序调用中使用用户模式驱动程序资源句柄。

用户模式运行时资源句柄和用户模式驱动程序资源句柄之间存在一对一的对应关系。 Direct3D 运行时和用户模式显示驱动程序通过[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)和[**D3DDDIARG\_OPENRESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)的**hResource**成员交换用户模式运行时和驱动程序资源句柄。构造.

当用户模式显示驱动程序调用 Direct3D 运行时的[**pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数来创建用户模式资源分配时，驱动程序应在**hResource**成员[**中指定用户模式运行时资源句柄。D3DDDICB\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate) *pData*参数所指向的结构。 Direct3D 运行时为资源生成唯一的内核模式句柄，并将其传递回 D3DDDICB\_分配的**hKMResource**成员中的用户模式显示驱动程序。 用户模式显示驱动程序可以在命令流中插入内核模式资源句柄，以便以后使用显示微型端口驱动程序。

**请注意**   虽然用户模式资源句柄对于每个用户模式资源创建始终是唯一的，但内核模式资源句柄并非始终唯一。 当 Direct3D 运行时调用用户模式显示驱动程序的[**OpenResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数来打开现有共享资源的视图时，运行时会在 D3DDDIARG 的**hKMResource**成员中传递资源的内核模式句柄[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource) *PResource*参数指向的 OPENRESOURCE 结构。 运行时先前在运行时创建了此内核模式句柄，调用了用户模式显示驱动程序的[**CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数。

 

若要销毁已创建*CreateResource*或*OpenResource*的用户模式资源，Direct3D 运行时在调用用户模式显示驱动程序的的 [**hResource 参数中传递用户模式驱动程序资源句柄DestroyResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)函数。 若要发布内核模式资源句柄以及与用户模式资源关联的所有分配，用户模式显示驱动程序会在 D3DDDICB 的**hResource**成员中传递用户模式运行时资源句柄[ **\_解除分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)在对[*pfnDeallocateCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)函数的调用中*pData*参数指向的结构。

当用户模式显示驱动程序创建和销毁资源时，请考虑以下各项：

-   对于用户模式显示驱动程序为响应共享资源而创建的分配（即，响应 D3DDDIARG\_**标志**成员中设置的**SharedResource**位字段标志的[**CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)调用[**CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)），驱动程序必须将非**NULL**值分配给[**D3DDDICB\_分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)的**hResource**成员。

-   对于用户模式显示驱动程序为响应非共享资源而创建的分配，驱动程序不需要将非**NULL**值分配给 D3DDDICB\_分配的**hResource**成员。 如果驱动程序将**NULL**分配给**hResource**，则分配将与设备相关联，而不是与特定资源（和内核模式资源句柄）相关联。 但是，如果分配确实与资源相关，则驱动程序应将分配与该资源关联起来。
    **请注意**   仅当用户模式显示驱动程序将\_D3DDDICB 的**hResource**成员设置为该驱动程序从 hResource 接收的用户模式运行时资源句柄时，才创建内核模式资源句柄。在对[**CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)的调用中， [**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的成员。

     

-   如果调用[**DestroyResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)来销毁非共享用户模式资源，则用户模式显示驱动程序可以调用[*pfnDeallocateCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb) ，并将[**D3DDDICB\_解除分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)设置为**NULL**的**hResource**成员仅在驱动程序永远不会将任何分配关联到资源。 如果用户模式显示驱动程序与资源分配相关联，则驱动程序必须使用 D3DDDICB\_解除分配设置为非**NULL**值的的**HResource**成员调用**pfnDeallocateCb** ;否则，会发生内存泄漏。

 

 





