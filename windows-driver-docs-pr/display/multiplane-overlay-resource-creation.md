---
title: 创建多平面覆盖资源
description: 使用 multiplane 覆盖时，这些要求适用于在 Microsoft DirectX apps 中创建的分配。
ms.assetid: B3E9BEF8-5CB8-45A3-9491-19AB1EA3D74F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f16e432683a88e865404aad3e61371a994e71150
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840542"
---
# <a name="multiplane-overlay-resource-creation"></a>创建多平面覆盖资源


使用 multiplane 覆盖时，这些要求适用于在 Microsoft DirectX apps 中创建的分配。

## <a name="span-iddirectx_11_resource_creationspanspan-iddirectx_11_resource_creationspanspan-iddirectx_11_resource_creationspandirectx-11-resource-creation"></a><span id="DirectX_11_resource_creation"></span><span id="directx_11_resource_creation"></span><span id="DIRECTX_11_RESOURCE_CREATION"></span>DirectX 11 资源创建


调用[*CreateResource （D3D11）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)函数时：

-   **D3D10\_ddi\_绑定\_存在**和**D3D10\_DDI\_资源\_杂项\_共享**常数值在 D3D11DDIARG 的**BindFlags**成员中设置[ **\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)结构，指示可对分配进行扫描。
-   还可能会设置**标志**中其他位字段标志，例如：
    -   **D3D10\_DDI\_绑定\_着色器\_资源**
    -   **D3D10\_DDI\_BIND\_RENDER\_目标**
    -   **D3D11\_DDI\_绑定\_无序\_访问**
    -   **D3D11\_DDI\_BIND\_解码器**
    -   **D3D11\_1DDI\_资源\_杂项\_受限\_内容**
    -   **D3D11\_1DDI\_资源\_杂项\_限制\_共享\_资源\_驱动程序**
-   在[*CreateResource （D3D11）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)调用中传递[**DXGI\_DDI 时\_主要\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)结构：
    -   [**DXGI\_DDI\_主\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)具有**VidPnSourceId**成员的适当值。
    -   [**DXGI\_DDI\_主\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)。**ModeDesc**匹配当前模式。
    -   对于 multiplane 覆盖资源，驱动程序不能将**dxgi\_DDI\_PRIMARY\_驱动程序\_标志，\_不**在 DXGI 的 DriverFlags 成员\_的成员\_[**主\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)。

## <a name="span-iddirectx_9_resource_creationspanspan-iddirectx_9_resource_creationspanspan-iddirectx_9_resource_creationspandirectx-9-resource-creation"></a><span id="DirectX_9_resource_creation"></span><span id="directx_9_resource_creation"></span><span id="DIRECTX_9_RESOURCE_CREATION"></span>DirectX 9 资源创建


调用[*CreateResource2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)函数时：

-   设置[**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构的**flags**成员**中的** **SharedResource**位字段标志。
-   还可能会设置**标志**中其他位字段标志，例如：
    -   **RenderTarget**
    -   **褐色**
    -   **DecodeRenderTarget**
    -   **RestrictedContent**
    -   **RestrictSharedAccess**
-   已正确初始化[**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构的**VidPnSourceId**成员。
-   [**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)结构的**RefreshRate**成员包含零。

 

 





