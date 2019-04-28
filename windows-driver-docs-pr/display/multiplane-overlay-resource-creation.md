---
title: 创建多平面覆盖资源
description: 当使用 multiplane 叠加时，这些要求适用于 Microsoft DirectX 应用中创建的分配。
ms.assetid: B3E9BEF8-5CB8-45A3-9491-19AB1EA3D74F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ac2cf5a648d676dc1580ad18ef2e77bfe6926c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345611"
---
# <a name="multiplane-overlay-resource-creation"></a>创建多平面覆盖资源


当使用 multiplane 叠加时，这些要求适用于 Microsoft DirectX 应用中创建的分配。

## <a name="span-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspandirectx-11-resource-creation"></a><span id="DirectX_11_resource_creation"></span><span id="directx_11_resource_creation"></span><span id="DIRECTX_11_RESOURCE_CREATION"></span>DirectX 11 资源创建


当[ *CreateResource(D3D11)* ](https://msdn.microsoft.com/library/windows/hardware/ff540694)调用函数：

-   **D3D10\_DDI\_绑定\_存在**并**D3D10\_DDI\_资源\_杂项\_共享**在中设置的常量值**BindFlags**的成员[ **D3D11DDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542062)结构，指示可以查看扫描分配。
-   可以在标记其他位域**标志**也将设置，如：
    -   **D3D10\_DDI\_绑定\_着色器\_资源**
    -   **D3D10\_DDI\_BIND\_RENDER\_TARGET**
    -   **D3D11\_DDI\_BIND\_UNORDERED\_ACCESS**
    -   **D3D11\_DDI\_BIND\_DECODER**
    -   **D3D11\_1DDI\_资源\_杂项\_RESTRICTED\_内容**
    -   **D3D11\_1DDI\_RESOURCE\_MISC\_RESTRICT\_SHARED\_RESOURCE\_DRIVER**
-   当[ **DXGI\_DDI\_主\_DESC** ](https://msdn.microsoft.com/library/windows/hardware/ff557511)结构传入[ *CreateResource(D3D11)*](https://msdn.microsoft.com/library/windows/hardware/ff540694)调用：
    -   [**DXGI\_DDI\_主\_DESC** ](https://msdn.microsoft.com/library/windows/hardware/ff557511)具有适当的值**VidPnSourceId**成员。
    -   [**DXGI\_DDI\_主\_DESC**](https://msdn.microsoft.com/library/windows/hardware/ff557511)。**ModeDesc**匹配的当前模式。
    -   对于 multiplane 覆盖资源，该驱动程序不设置**DXGI\_DDI\_主\_驱动程序\_标志\_否\_SCANOUT**标志中值**DriverFlags**的成员[ **DXGI\_DDI\_主\_DESC**](https://msdn.microsoft.com/library/windows/hardware/ff557511)。

## <a name="span-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspandirectx-9-resource-creation"></a><span id="DirectX_9_resource_creation"></span><span id="directx_9_resource_creation"></span><span id="DIRECTX_9_RESOURCE_CREATION"></span>DirectX 9 资源创建


当[ *CreateResource2* ](https://msdn.microsoft.com/library/windows/hardware/hh406287)调用函数：

-   **主**并**SharedResource**标记中的位域**标志**隶属[ **D3DDDIARG\_CREATERESOURCE2** ](https://msdn.microsoft.com/library/windows/hardware/hh451074)结构设置。
-   可以在标记其他位域**标志**也将设置，如：
    -   **RenderTarget**
    -   **纹理**
    -   **DecodeRenderTarget**
    -   **RestrictedContent**
    -   **RestrictSharedAccess**
-   **VidPnSourceId**的成员[ **D3DDDIARG\_CREATERESOURCE2** ](https://msdn.microsoft.com/library/windows/hardware/hh451074)结构正确初始化。
-   **RefreshRate**的成员[ **D3DDDIARG\_CREATERESOURCE2** ](https://msdn.microsoft.com/library/windows/hardware/hh451074)结构包含零。

 

 





