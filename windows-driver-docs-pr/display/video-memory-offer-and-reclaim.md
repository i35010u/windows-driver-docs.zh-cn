---
title: 视频内存供应和回收
description: Windows 显示驱动程序模型（WDDM）1.2 和更高版本的用户模式显示驱动程序必须使用从 Windows 8 开始提供的内存提供和回收功能，以减少本地和系统内存中的临时表面所需的内存开销。
ms.assetid: 8BB6A7A3-E102-4069-BFC2-9605DDE9F020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cdfda6e350753a70edb0d9e0a1af8a56aef1082
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825293"
---
# <a name="video-memory-offer-and-reclaim"></a>视频内存供应和回收


Windows 显示驱动程序模型（WDDM）1.2 和更高版本的用户模式显示驱动程序必须使用从 Windows 8 开始提供的内存提供和回收功能，以减少本地和系统内存中的临时表面所需的内存开销。

|                                                                                   |                                  |
|-----------------------------------------------------------------------------------|----------------------------------|
| 最小 WDDM 版本                                                              | 1.2                              |
| 最大 Windows 版本                                                           | 8                                |
| 驱动程序实现-仅限完整图形和呈现                               | Mandatory                        |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | **设备 。OfferReclaim** |

 

尤其是在移动方案中，需要硬件加速的图形密集型应用程序可能会大量使用 GPU 资源。 此外，在许多移动设备中，GPU 都集成到 CPU 芯片中，GPU 使用部分系统内存作为视频内存。 为了确保在多个应用程序大量使用 GPU 时，这些应用程序会对系统内存造成大量需求，应将显示驱动程序的内存占用量降到最低。 提议/回收设备驱动程序接口（DDIs）提供了执行此操作的机制。

应用程序可使用 API 提供不需要的内存，系统稍后可为其他用途回收，并回收最近丢弃的内存。 请参阅 Microsoft DirectX 图形基础结构（DXGI）应用编程主题： [DXGI 1.2 改进](https://docs.microsoft.com/windows/desktop/direct3ddxgi/dxgi-1-2-improvements)。

## <a name="span-idoffer_and_reclaim_ddispanspan-idoffer_and_reclaim_ddispanspan-idoffer_and_reclaim_ddispanoffer-and-reclaim-ddi"></a><span id="Offer_and_reclaim_DDI"></span><span id="offer_and_reclaim_ddi"></span><span id="OFFER_AND_RECLAIM_DDI"></span>提供和回收 DDI


从 Windows 8 开始提供了新函数，以供用户模式驱动程序提供或回收内存。

驱动程序调用这些系统提供的函数来提供或回收内存分配：

-   [**pfnOfferAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocationscb)
-   [**pfnReclaimAllocationsCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)

如果驱动程序支持 Microsoft Direct3D 10 硬件，则该驱动程序会实现这些功能：

-   [*pfnOfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*pfnReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

如果驱动程序支持 Microsoft Direct3D 9 硬件，则该驱动程序会实现以下功能。 此外，如果应用在 Direct3D 9 硬件上运行的 Direct3D 11 API 提供或回收其分配，Direct3D 运行时将调用以下函数：

-   [*OfferResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*ReclaimResources*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimresources)

使用这些关联的结构和枚举：

-   [**D3DDDI\_提供\_优先级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddi_offer_priority)
-   [**D3DDDIARG\_OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_offerresources)
-   [**D3DDDIARG\_RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_reclaimresources)
-   [**D3DDDICB\_OFFERALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_offerallocations)
-   [**D3DDDICB\_RECLAIMALLOCATIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations)
-   [**DXGI\_DDI\_ARG\_OFFERRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_offerresources)
-   [**DXGI\_DDI\_ARG\_RECLAIMRESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_reclaimresources)
-   [**DXGI1\_2\_DDI\_基\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

为了支持产品/服务功能，从 Windows 8 开始，此结构有两个新成员：

-   [**D3DDDI\_ALLOCATIONLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationlist)

你应仔细测试驱动程序是否正确处理此功能，因为在放弃分配之后，其中的所有数据都将丢失。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit) **OfferReclaim**。 请注意，这些要求列出了驱动程序必须提供分配的方案。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)，了解 Windows 8 中添加的功能。

 

 





