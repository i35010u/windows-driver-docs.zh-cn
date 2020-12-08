---
title: 视频内存供应和回收
description: Windows 显示驱动程序模型 (WDDM) 1.2 及更高版本的用户模式显示驱动程序必须使用从 Windows 8 开始提供的内存提供和回收功能，以减少本地和系统内存中的临时表面所需的内存开销。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42fe110b62b4976a83562c77283803530c6a2dc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802503"
---
# <a name="video-memory-offer-and-reclaim"></a>视频内存供应和回收


Windows 显示驱动程序模型 (WDDM) 1.2 及更高版本的用户模式显示驱动程序必须使用从 Windows 8 开始提供的内存提供和回收功能，以减少本地和系统内存中的临时表面所需的内存开销。

**最小 WDDM 版本**：1。2

**最低 Windows 版本**：8

**驱动程序实现-完整图形和仅呈现**：必需

**[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试**：**设备 .。。OfferReclaim**


 

尤其是在移动方案中，需要硬件加速的图形密集型应用程序可能会大量使用 GPU 资源。 此外，在许多移动设备中，GPU 都集成到 CPU 芯片中，GPU 使用部分系统内存作为视频内存。 为了确保在多个应用程序大量使用 GPU 时，这些应用程序会对系统内存造成大量需求，应将显示驱动程序的内存占用量降到最低。 提议/回收设备驱动程序接口 (DDIs) 提供一种机制来实现此目的。

应用程序可使用 API 提供不需要的内存，系统稍后可为其他用途回收，并回收最近丢弃的内存。 请参阅 Microsoft DirectX 图形基础结构 (DXGI) 应用编程主题， [dxgi 1.2 改进](/windows/desktop/direct3ddxgi/dxgi-1-2-improvements)。

## <a name="span-idoffer_and_reclaim_ddispanspan-idoffer_and_reclaim_ddispanspan-idoffer_and_reclaim_ddispanoffer-and-reclaim-ddi"></a><span id="Offer_and_reclaim_DDI"></span><span id="offer_and_reclaim_ddi"></span><span id="OFFER_AND_RECLAIM_DDI"></span>提供和回收 DDI


从 Windows 8 开始提供了新函数，以供用户模式驱动程序提供或回收内存。

驱动程序调用这些系统提供的函数来提供或回收内存分配：

-   [**pfnOfferAllocationsCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocationscb)
-   [**pfnReclaimAllocationsCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocationscb)

如果驱动程序支持 Microsoft Direct3D 10 硬件，则该驱动程序会实现这些功能：

-   [*pfnOfferResources*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*pfnReclaimResources*](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

如果驱动程序支持 Microsoft Direct3D 9 硬件，则该驱动程序会实现以下功能。 此外，如果应用在 Direct3D 9 硬件上运行的 Direct3D 11 API 提供或回收其分配，Direct3D 运行时将调用以下函数：

-   [*OfferResources*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerresources)
-   [*ReclaimResources*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimresources)

使用这些关联的结构和枚举：

-   [**D3DDDI \_ 产品/服务 \_ 优先级**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddi_offer_priority)
-   [**D3DDDIARG \_ OFFERRESOURCES**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_offerresources)
-   [**D3DDDIARG \_ RECLAIMRESOURCES**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_reclaimresources)
-   [**D3DDDICB \_ OFFERALLOCATIONS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_offerallocations)
-   [**D3DDDICB \_ RECLAIMALLOCATIONS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations)
-   [**DXGI \_ DDI \_ ARG \_ OFFERRESOURCES**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_offerresources)
-   [**DXGI \_ DDI \_ ARG \_ RECLAIMRESOURCES**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_reclaimresources)
-   [**DXGI1 \_ 2 \_ DDI \_ 基本 \_ 函数**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

为了支持产品/服务功能，从 Windows 8 开始，此结构有两个新成员：

-   [**D3DDDI \_ ALLOCATIONLIST**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationlist)

你应仔细测试驱动程序是否正确处理此功能，因为在放弃分配之后，其中的所有数据都将丢失。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) **OfferReclaim**。 请注意，这些要求列出了驱动程序必须提供分配的方案。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

 

