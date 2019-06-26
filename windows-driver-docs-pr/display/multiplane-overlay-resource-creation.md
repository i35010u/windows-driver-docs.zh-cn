---
title: 创建多平面覆盖资源
description: 当使用 multiplane 叠加时，这些要求适用于 Microsoft DirectX 应用中创建的分配。
ms.assetid: B3E9BEF8-5CB8-45A3-9491-19AB1EA3D74F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d43313e095836a28dd1a2b36976105ef341e74b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372845"
---
# <a name="multiplane-overlay-resource-creation"></a>创建多平面覆盖资源


当使用 multiplane 叠加时，这些要求适用于 Microsoft DirectX 应用中创建的分配。

## <a name="span-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspandirectx-11-resource-creation"></a><span id="DirectX_11_resource_creation"></span><span id="directx_11_resource_creation"></span><span id="DIRECTX_11_RESOURCE_CREATION"></span>DirectX 11 资源创建


当[ *CreateResource(D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)调用函数：

-   **D3D10\_DDI\_绑定\_存在**并**D3D10\_DDI\_资源\_杂项\_共享**在中设置的常量值**BindFlags**的成员[ **D3D11DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)结构，指示可以查看扫描分配。
-   可以在标记其他位域**标志**也将设置，如：
    -   **D3D10\_DDI\_绑定\_着色器\_资源**
    -   **D3D10\_DDI\_BIND\_RENDER\_TARGET**
    -   **D3D11\_DDI\_BIND\_UNORDERED\_ACCESS**
    -   **D3D11\_DDI\_BIND\_DECODER**
    -   **D3D11\_1DDI\_资源\_杂项\_RESTRICTED\_内容**
    -   **D3D11\_1DDI\_RESOURCE\_MISC\_RESTRICT\_SHARED\_RESOURCE\_DRIVER**
-   当[ **DXGI\_DDI\_主\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)结构传入[ *CreateResource(D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)调用：
    -   [**DXGI\_DDI\_主\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)具有适当的值**VidPnSourceId**成员。
    -   [**DXGI\_DDI\_主\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)。**ModeDesc**匹配的当前模式。
    -   对于 multiplane 覆盖资源，该驱动程序不设置**DXGI\_DDI\_主\_驱动程序\_标志\_否\_SCANOUT**标志中值**DriverFlags**的成员[ **DXGI\_DDI\_主\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)。

## <a name="span-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspandirectx-9-resource-creation"></a><span id="DirectX_9_resource_creation"></span><span id="directx_9_resource_creation"></span><span id="DIRECTX_9_RESOURCE_CREATION"></span>DirectX 9 资源创建


当[ *CreateResource2* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)调用函数：

-   **主**并**SharedResource**标记中的位域**标志**隶属[ **D3DDDIARG\_CREATERESOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构设置。
-   可以在标记其他位域**标志**也将设置，如：
    -   **RenderTarget**
    -   **纹理**
    -   **DecodeRenderTarget**
    -   **RestrictedContent**
    -   **RestrictSharedAccess**
-   **VidPnSourceId**的成员[ **D3DDDIARG\_CREATERESOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构正确初始化。
-   **RefreshRate**的成员[ **D3DDDIARG\_CREATERESOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构包含零。

 

 





