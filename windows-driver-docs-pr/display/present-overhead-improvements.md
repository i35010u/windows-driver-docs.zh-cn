---
title: 呈现开销提高
ms.assetid: 92B282D6-0D04-4352-AE03-E0A7A43711E7
description: 对内部交换缓冲区的改进，以减少 GPU 处理负载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e158d0fdff1c1a5ab75bca334c4e73b233f3f067
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829713"
---
# <a name="present-overhead-improvements"></a>呈现开销提高


从 Windows 8.1 开始，Microsoft Direct3D 运行时更有效地处理内部交换缓冲区，从而减少 GPU 上的处理负载。 为了支持这种更好的性能，Windows 显示驱动程序模型（WDDM）1.3 和更高版本的驱动程序必须支持新的现有设备驱动程序接口（DDI）和新的纹理格式作为共享表面：

## <a name="span-idwddm_13_present_ddispanspan-idwddm_13_present_ddispanwddm-13-present-ddi"></a><span id="wddm_1.3_present_ddi"></span><span id="WDDM_1.3_PRESENT_DDI"></span>WDDM 1.3 存在 DDI


以下参考主题介绍如何在显示微型端口驱动程序和用户模式显示驱动程序中实现此功能：

-   [*pfnPresent1 （D3D）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present1)
-   [*pfnPresent1 （DXGI）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)
-   [**D3DDDIARG\_PRESENT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_present1)
-   [**D3DDDIARG\_PRESENTSURFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_presentsurface)
-   [**D3DKMT\_组合\_PRESENTHISTORYTOKEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_composition_presenthistorytoken)
-   [**DXGI\_DDI\_ARG\_PRESENT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present1)
-   [**DXGI\_DDI\_ARG\_PRESENTSURFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_presentsurface)
-   [**D3DDDI\_DEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) （new **pfnPresent1**函数指针）
-   [**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat) （new **D3DDDIFMT\_G8R8**和**D3DDDIFMT\_R8**常量值）
-   [**D3DKMT\_提供\_模型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ne-d3dkmthk-_d3dkmt_present_model)（new **D3DKMT\_PM\_重定向\_组合**常数值）
-   [**D3DKMT\_PRESENTHISTORYTOKEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presenthistorytoken) （新建**组合**成员）
-   [**DXGI\_DDI\_基本\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)（new **pDXGIDDIBaseFunctions4**成员）
-   [**DXGI1\_3\_DDI\_基\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)（new **pfnPresent1**函数指针）

## <a name="span-idtexture_format_support_for_shared_surfacesspanspan-idtexture_format_support_for_shared_surfacesspanspan-idtexture_format_support_for_shared_surfacesspantexture-format-support-for-shared-surfaces"></a><span id="Texture_format_support_for_shared_surfaces"></span><span id="texture_format_support_for_shared_surfaces"></span><span id="TEXTURE_FORMAT_SUPPORT_FOR_SHARED_SURFACES"></span>共享图面的纹理格式支持


驱动程序应支持从[**DXGI\_格式**](https://docs.microsoft.com/windows/desktop/api/dxgiformat/ne-dxgiformat-dxgi_format)枚举中共享资源和可共享的 backbuffers：

- **DXGI\_格式\_A8\_UNORM**
- **DXGI\_格式\_R8\_UNORM**
- **DXGI\_格式\_R8G8\_UNORM**
- **DXGI\_格式\_BC1\_无格式\\** *
- **DXGI\_格式\_BC1\_UNORM**
- **DXGI\_格式\_BC1\_UNORM\_SRGB**
- **DXGI\_格式\_BC2\_无格式\\** *
- **DXGI\_格式\_BC2\_UNORM**
- **DXGI\_格式\_BC2\_UNORM\_SRGB**
- **DXGI\_格式\_BC3\_无格式\\** *
- **DXGI\_格式\_BC3\_UNORM**
- **DXGI\_格式\_BC3\_UNORM\_SRGB**

此外，如果驱动程序在 Direct3D 功能级别9硬件上支持 Microsoft Direct3D 11 及更高版本，则这些驱动程序应支持**DXGI\_格式\_L8\_UNORM**占位符格式。 **\_L8\_UNORM 的 DXGI\_格式**与**D3DDDIFMT\_L8**格式的功能相同。

驱动程序还应支持[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举中的其他纹理格式：

-   **D3DDDIFMT\_G8R8**
-   **D3DDDIFMT\_R8**

 

 





