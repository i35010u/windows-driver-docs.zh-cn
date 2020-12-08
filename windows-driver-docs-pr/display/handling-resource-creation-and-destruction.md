---
title: 处理资源创建和销毁
description: 处理资源创建和销毁
keywords:
- 资源创建 WDK 显示
- 资源销毁 WDK 显示
- 销毁资源 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7454594c7aae0d272af84306a36ed42575fe0da3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813231"
---
# <a name="handling-resource-creation-and-destruction"></a>处理资源创建和销毁


若要使 Microsoft DirectX 图形内核子系统能够正确跟踪资源生存期并在操作系统中阻止内存泄漏，用户模式显示驱动程序必须正确创建和销毁资源。

Microsoft Direct3D 运行时调用以下用户模式显示驱动程序函数来创建用户模式资源。

-   [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 创建新的共享或非共享资源。

-   [**OpenResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource) 打开现有共享资源的视图。

在这两次调用中，Direct3D 运行时传递唯一的 *用户模式运行时资源句柄* ，用户模式显示驱动程序使用该句柄回调到运行时。 当 *CreateResource* 或 *OpenResource* 成功返回时，用户模式显示驱动程序将返回表示资源的唯一用户模式句柄。 此句柄是 *用户模式驱动程序资源句柄*。 运行时在后续的驱动程序调用中使用用户模式驱动程序资源句柄。

用户模式运行时资源句柄和用户模式驱动程序资源句柄之间存在一对一的对应关系。 Direct3D 运行时和用户模式显示驱动程序通过 [**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)和 [**D3DDDIARG \_ OPENRESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)结构的 **hResource** 成员交换用户模式运行时和驱动程序资源句柄。

当用户模式显示驱动程序调用 Direct3D 运行时的 [**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数来创建用户模式资源分配时，驱动程序应在 *pData* 参数指向的 [**D3DDDICB \_ 分配**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)结构的 **hResource** 成员中指定用户模式运行时资源句柄。 Direct3D 运行时为资源生成唯一的内核模式句柄，并将其传递回 D3DDDICB 分配的 **hKMResource** 成员中的用户模式显示驱动程序 \_ 。 用户模式显示驱动程序可以在命令流中插入内核模式资源句柄，以便以后使用显示微型端口驱动程序。

**注意**   尽管用户模式资源句柄对于每个用户模式资源创建始终是唯一的，但内核模式资源句柄并非始终唯一。 当 Direct3D 运行时调用用户模式显示驱动程序的 [**OpenResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数来打开现有共享资源的视图时，运行时将在 *pResource* 参数指向的 [**D3DDDIARG \_ OpenResource**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)结构的 **hKMResource** 成员中传递资源的内核模式句柄。 运行时先前在运行时创建了此内核模式句柄，调用了用户模式显示驱动程序的 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 函数。

 

若要销毁已创建 *CreateResource* 或 *OpenResource* 的用户模式资源，Direct3D 运行时在调用用户模式显示驱动程序的 [**DestroyResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)函数的 *hResource* 参数中传递用户模式驱动程序资源句柄。 若要发布内核模式资源句柄以及与用户模式资源关联的所有分配，用户模式显示驱动程序将传递 *pData* 参数在调用 [*PfnDeallocateCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)函数的 [**D3DDDICB \_ 释放**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)结构的 **hResource** 成员中的用户模式运行时资源句柄。

当用户模式显示驱动程序创建和销毁资源时，请考虑以下各项：

-   对于用户模式显示驱动程序为响应共享资源而创建的分配 (也就是说，为了响应 [**D3DDDIARG \_ CreateResource**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)) **标志** 成员中设置 **的 SharedResource** 位字段标志的 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)调用，驱动程序必须将非 **NULL** 值分配给 [**hResource \_ 分配**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)的 **D3DDDICB** 成员。

-   对于用户模式显示驱动程序为响应非共享资源而创建的分配，驱动程序不需要将非 **NULL** 值分配给 D3DDDICB 分配的 **hResource** 成员 \_ 。 如果驱动程序将 **NULL** 分配给 **hResource**，则分配将与设备相关联，而不是特定资源 (和内核模式资源句柄) 。 但是，如果分配确实与资源相关，则驱动程序应将分配与该资源关联起来。
    **注意**  仅当用户模式显示驱动程序将 D3DDDICB 分配的 **hResource** 成员设置 \_ 为用户模式运行时资源句柄时， **hResource** [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)才会创建内核模式资源句柄，驱动程序会将分配给驱动 [**程序 \_**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource) 。

     

-   如果调用 [**DestroyResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)来销毁非共享用户模式资源，则只有当驱动程序永远不与资源的任何分配关联时，用户模式显示驱动程序才能调用 [*pfnDeallocateCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb) ，并将 [**D3DDDICB \_ 解除分配**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)的 **hResource** 成员设置为 **NULL** 。 如果用户模式显示驱动程序与资源的分配相关联，则驱动程序必须调用 **pfnDeallocateCb** ，并将 D3DDDICB 解除关联的 **hResource** 成员 \_ 设置为非 **NULL** 值; 否则，会发生内存泄漏。

 

