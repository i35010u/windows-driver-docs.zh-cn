---
title: 视频内存供应和回收
description: Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本的用户模式显示驱动程序必须使用的内存产品/服务，并回收功能，从 Windows 8 中，以减少内存开销所需的临时应用层协议在本地和系统内存中开始提供。
ms.assetid: 8BB6A7A3-E102-4069-BFC2-9605DDE9F020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c03386efab6f3bd9d98d798b0f6ca522be330539
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365078"
---
# <a name="video-memory-offer-and-reclaim"></a>视频内存供应和回收


Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本的用户模式显示驱动程序必须使用的内存产品/服务，并回收功能，从 Windows 8 中，以减少内存开销所需的临时应用层协议在本地和系统内存中开始提供。

|                                                                                   |                                  |
|-----------------------------------------------------------------------------------|----------------------------------|
| WDDM 的最低版本                                                              | 1.2                              |
| 最大 Windows 版本                                                           | 8                                |
| 驱动程序实现 — 仅完全图形和呈现                               | 强制                        |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | **Device.Graphics...OfferReclaim** |

 

尤其是在移动方案，需要硬件加速的图形密集型应用程序可以使用大量 GPU 资源。 此外，在很多移动设备中 GPU 已集成到 CPU 芯片集，GPU 为视频内存使用的系统内存的部分。 若要确保合理的系统性能，当多个应用程序进行大量使用 GPU 反过来对所做的大量需求系统内存时，显示器驱动程序的内存占用应最小化。 产品/服务回收/设备驱动程序接口 (DDIs) 提供一种机制来执行此操作。

一个 API，可用于应用程序提供更高版本，系统可以回收有关其他用法，以及关于回收最近已被丢弃的内存的不需要的内存。 请参阅 Microsoft DirectX 图形基础结构 (DXGI) 应用编程主题[DXGI 1.2 改进](https://docs.microsoft.com/windows/desktop/direct3ddxgi/dxgi-1-2-improvements)。

## <a name="span-idofferandreclaimddispanspan-idofferandreclaimddispanspan-idofferandreclaimddispanoffer-and-reclaim-ddi"></a><span id="Offer_and_reclaim_DDI"></span><span id="offer_and_reclaim_ddi"></span><span id="OFFER_AND_RECLAIM_DDI"></span>提供和回收 DDI


可从产品/服务或回收内存的用户模式驱动程序的 Windows 8 开始新的函数。

该驱动程序将调用这些系统提供的函数来提供或回收内存分配：

-   [**pfnOfferAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocationscb)
-   [**pfnReclaimAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)

如果它支持 Microsoft Direct3D 10 硬件，该驱动程序实现这些函数：

-   [*pfnOfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*pfnReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

该驱动程序实现以下函数，如果它支持 Microsoft Direct3D 9 的硬件。 此外，如果应用程序产品/服务，或使用 Direct3D 11 API Direct3D 9 的硬件上运行的同时回收其分配，Direct3D 运行时调用这些函数：

-   [*OfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*ReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimresources)

使用这些关联的结构和枚举：

-   [**D3DDDI\_OFFER\_PRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddi_offer_priority)
-   [**D3DDDIARG\_OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_offerresources)
-   [**D3DDDIARG\_RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_reclaimresources)
-   [**D3DDDICB\_OFFERALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_offerallocations)
-   [**D3DDDICB\_RECLAIMALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations)
-   [**DXGI\_DDI\_ARG\_OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_offerresources)
-   [**DXGI\_DDI\_ARG\_RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_reclaimresources)
-   [**DXGI1\_2\_DDI\_BASE\_FUNCTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

若要支持的产品/服务/回收功能，从 Windows 8 开始此结构具有两个新成员：

-   [**D3DDDI\_ALLOCATIONLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationlist)

您应仔细测试，您的驱动程序处理此功能正确因为放弃分配后，在其中的所有数据都都会丢失。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...OfferReclaim**。 请注意，这些要求列出驱动程序必须在其中提供分配的方案。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





