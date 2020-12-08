---
title: 创建多平面覆盖资源
description: 使用 multiplane 覆盖时，这些要求适用于在 Microsoft DirectX apps 中创建的分配。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abddac83a60e3d0b2af517c5ca31ca31c0f8a7f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816333"
---
# <a name="multiplane-overlay-resource-creation"></a>创建多平面覆盖资源


使用 multiplane 覆盖时，这些要求适用于在 Microsoft DirectX apps 中创建的分配。

## <a name="span-iddirectx_11_resource_creationspanspan-iddirectx_11_resource_creationspanspan-iddirectx_11_resource_creationspandirectx-11-resource-creation"></a><span id="DirectX_11_resource_creation"></span><span id="directx_11_resource_creation"></span><span id="DIRECTX_11_RESOURCE_CREATION"></span>DirectX 11 资源创建


调用 [*CreateResource (D3D11)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource) 函数时：

-   **D3D10 \_ ddi \_ BIND \_ 存在**， **D3D10 \_ ddi \_ 资源 \_ 杂项 \_ 共享** 常数值是在 [**D3D11DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)结构的 **BindFlags** 成员中设置的，指示可以通过扫描分配。
-   还可能会设置 **标志** 中其他位字段标志，例如：
    -   **D3D10 \_ DDI \_ BIND \_ 着色器 \_ 资源**
    -   **D3D10 \_ DDI \_ 绑定 \_ 呈现器 \_ 目标**
    -   **D3D11 \_ DDI \_ 绑定 \_ 无序 \_ 访问**
    -   **D3D11 \_ DDI \_ BIND \_ 解码器**
    -   **D3D11 \_ 1DDI \_ 资源 \_ 杂项 \_ 受限 \_ 内容**
    -   **D3D11 \_ 1DDI \_ 资源 \_ 杂项 \_ 限制 \_ 共享 \_ 资源 \_ 驱动程序**
-   当在 [*CreateResource (D3D11)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)调用中传递 [**DXGI \_ DDI \_ PRIMARY \_ DESC**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)结构时：
    -   [**DXGI \_DDI \_ 主要 \_ DESC**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc) 具有适用于 **VidPnSourceId** 成员的值。
    -   [**DXGI \_DDI \_ 主要 \_ DESC**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)。**ModeDesc** 匹配当前模式。
    -   对于 multiplane 覆盖资源，驱动程序不能在 [**dxgi \_ ddi \_ Primary \_ DESC**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)的 **DriverFlags** 成员中设置 **dxgi \_ ddi \_ 主 \_ 驱动程序 \_ 标志 \_ NO \_ SCANOUT** 标志值。

## <a name="span-iddirectx_9_resource_creationspanspan-iddirectx_9_resource_creationspanspan-iddirectx_9_resource_creationspandirectx-9-resource-creation"></a><span id="DirectX_9_resource_creation"></span><span id="directx_9_resource_creation"></span><span id="DIRECTX_9_RESOURCE_CREATION"></span>DirectX 9 资源创建


调用 [*CreateResource2*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2) 函数时：

-   设置 [**D3DDDIARG \_ CREATERESOURCE2**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构的 **flags** **成员的** **SharedResource** 位字段标志。
-   还可能会设置 **标志** 中其他位字段标志，例如：
    -   **RenderTarget**
    -   **纹理**
    -   **DecodeRenderTarget**
    -   **RestrictedContent**
    -   **RestrictSharedAccess**
-   [**D3DDDIARG \_ CREATERESOURCE2**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构的 **VidPnSourceId** 成员已正确初始化。
-   [**D3DDDIARG \_ CREATERESOURCE2**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构的 **RefreshRate** 成员包含零。

 

