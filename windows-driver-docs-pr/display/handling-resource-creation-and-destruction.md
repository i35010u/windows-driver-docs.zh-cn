---
title: 处理资源创建和销毁
description: 处理资源创建和销毁
ms.assetid: d443bdc3-1c5a-4372-9e6a-b8a4d21499b9
keywords:
- 资源创建 WDK 显示
- 资源析构 WDK 显示
- 销毁 WDK 显示的资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbaefd1d31f75ce9b05d9103e4fe8a34e9556f8a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369869"
---
# <a name="handling-resource-creation-and-destruction"></a>处理资源创建和销毁


若要启用 Microsoft DirectX 图形内核子系统以正确跟踪资源的生存期并防止内存泄漏操作系统用户模式中的显示器驱动程序必须正确创建和销毁资源。

Microsoft Direct3D 运行时调用以下用户模式显示驱动程序函数来创建用户模式下的资源。

-   [**CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)创建了新的共享或取消共享资源。

-   [**OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)打开现有的共享资源的视图。

在这两个调用中，Direct3D 运行时将传递的唯一*用户模式下运行时资源句柄*用户模式显示驱动程序用来回调到运行时。 当*CreateResource*或*OpenResource*成功，则返回用户模式显示驱动程序返回一个表示资源的唯一用户模式句柄。 此句柄*用户模式驱动程序的资源句柄*。 运行时在后续的驱动程序调用中使用用户模式驱动程序的资源句柄。

用户模式下运行时资源句柄和用户模式驱动程序的资源句柄之间存在一对一的对应关系。 Direct3D 运行时和用户模式下显示的用户模式下运行时和驱动程序资源处理通过驱动程序 exchange **hResource**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)并[ **D3DDDIARG\_OPENRESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)结构。

当用户模式显示驱动程序调用 Direct3D 运行时[ **pfnAllocateCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数创建的用户模式资源分配，该驱动程序应指定用户模式下运行时资源在中处理**hResource**的成员[ **D3DDDICB\_分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)结构*pData*参数指向。 Direct3D 运行时生成唯一的内核模式资源的句柄并传递回用户模式下显示中的驱动程序**hKMResource** D3DDDICB 成员\_分配。 用户模式显示驱动程序可以在显示的微型端口驱动程序，以供以后使用的命令流中插入的内核模式资源句柄。

**请注意**  用户模式资源句柄始终是针对每个用户模式资源创建唯一的尽管内核模式资源句柄并不总是唯一。 当 Direct3D 运行时调用用户模式显示驱动程序[ **OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数打开的视图到现有共享资源，请在运行时将资源的内核模式句柄传递中**hKMResource**的成员[ **D3DDDIARG\_OPENRESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)结构*pResource*参数指向。 在运行时之前创建此内核模式句柄后调用用户模式显示驱动程序的运行时[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数。

 

若要销毁用户模式资源的*CreateResource*或*OpenResource*创建，Direct3D 运行时将传递用户模式驱动程序的资源句柄中*hResource*对用户模式显示驱动程序的调用中的参数[ **DestroyResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)函数。 若要释放的内核模式资源句柄和所有与用户模式资源相关联的分配，用户模式显示驱动程序，将传递中的用户模式下运行时资源句柄**hResource** 的成员[**D3DDDICB\_DEALLOCATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)结构的*pData*参数指向调用[ *pfnDeallocateCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)函数。

在用户模式显示驱动程序创建和销毁资源时，请考虑以下各项：

-   对于用户模式显示驱动程序创建的共享资源的响应中的分配 (即，在响应[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)使用调用**SharedResource**在中设置的位域标志**标志**的成员[ **D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource))，该驱动程序必须将分配一个非**NULL**值设为**hResource**的成员[ **D3DDDICB\_分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)。

-   对于用户模式显示驱动程序创建对非共享资源的响应中的分配，该驱动程序不需要分配一个非**NULL**值设置为**hResource** D3DDDICB 成员\_分配。 如果该驱动程序将分配**NULL**到**hResource**，分配是与设备并不特定资源 （和内核模式资源句柄） 相关联。 但是，如果真正与资源相关的分配，该驱动程序应与该资源关联分配。
    **请注意**  仅当用户模式显示驱动程序集创建内核模式资源句柄**hResource** D3DDDICB 成员\_分配到用户模式下运行时资源处理驱动程序从收到**hResource**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)中调用的结构[ **CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)。

     

-   当[ **DestroyResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)调用要销毁的非共享的用户模式资源，用户模式显示驱动程序可以调用[ *pfnDeallocateCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)与**hResource**的成员[ **D3DDDICB\_DEALLOCATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)设置为**NULL**仅当驱动程序永远不会与资源关联任何分配。 如果用户模式显示驱动程序与资源相关联的分配，该驱动程序必须调用**pfnDeallocateCb**与**hResource** D3DDDICB 成员\_设置为非DEALLOCATE**NULL**值; 否则，将发生内存泄漏。

 

 





