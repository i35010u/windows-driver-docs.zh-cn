---
title: 呈现开销提高
ms.assetid: 92B282D6-0D04-4352-AE03-E0A7A43711E7
description: 对内部交换缓冲区的改进，以减少 GPU 处理负载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3db9b57122c994d496782f26d1577978039ff6ad
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715154"
---
# <a name="present-overhead-improvements"></a>呈现开销提高


从 Windows 8.1 开始，Microsoft Direct3D 运行时更有效地处理内部交换缓冲区，从而减少 GPU 上的处理负载。 为了支持这种更好的性能，Windows 显示驱动程序模型 (WDDM) 1.3 及更高版本的驱动程序必须支持新的现有设备驱动程序接口 (DDI) 并将新的纹理格式作为共享表面：

## <a name="span-idwddm_13_present_ddispanspan-idwddm_13_present_ddispanwddm-13-present-ddi"></a><span id="wddm_1.3_present_ddi"></span><span id="WDDM_1.3_PRESENT_DDI"></span>WDDM 1.3 存在 DDI


以下参考主题介绍如何在显示微型端口驱动程序和用户模式显示驱动程序中实现此功能：

-   [*pfnPresent1 (D3D) *](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present1)
-   [*pfnPresent1 (DXGI) *](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)
-   [**D3DDDIARG \_ PRESENT1**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_present1)
-   [**D3DDDIARG \_ PRESENTSURFACE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_presentsurface)
-   [**D3DKMT \_ 组合 \_ PRESENTHISTORYTOKEN**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_composition_presenthistorytoken)
-   [**DXGI \_ DDI \_ ARG \_ PRESENT1**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present1)
-   [**DXGI \_ DDI \_ ARG \_ PRESENTSURFACE**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_presentsurface)
-   [**D3DDDI \_DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) (New **pfnPresent1** 函数指针) 
-   [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat) (new **D3DDDIFMT \_ G8R8** 和 **D3DDDIFMT \_ R8** 常量值) 
-   [**D3DKMT \_现有 \_ 模型**](/windows-hardware/drivers/ddi/d3dkmthk/ne-d3dkmthk-_d3dkmt_present_model) (新 **D3DKMT \_ PM \_ 重定向 \_ 组合** 常数值) 
-   [**D3DKMT \_PRESENTHISTORYTOKEN**](/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presenthistorytoken) (新的 **撰写** 成员) 
-   [**DXGI \_DDI \_ 基 \_ 参数**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args) (new **pDXGIDDIBaseFunctions4** 成员) 
-   [**DXGI1 \_ 3 \_ DDI \_ 基本 \_ 函数**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions) (new **pfnPresent1** 函数指针) 

## <a name="span-idtexture_format_support_for_shared_surfacesspanspan-idtexture_format_support_for_shared_surfacesspanspan-idtexture_format_support_for_shared_surfacesspantexture-format-support-for-shared-surfaces"></a><span id="Texture_format_support_for_shared_surfaces"></span><span id="texture_format_support_for_shared_surfaces"></span><span id="TEXTURE_FORMAT_SUPPORT_FOR_SHARED_SURFACES"></span>共享图面的纹理格式支持


驱动程序应支持从 [**DXGI \_ 格式**](/windows/win32/api/dxgiformat/ne-dxgiformat-dxgi_format) 枚举共享资源和可共享的 backbuffers：

- **DXGI \_ 格式 \_ A8 \_ UNORM**
- **DXGI \_ FORMAT \_ R8 \_ UNORM**
- **DXGI \_ FORMAT \_ R8G8 \_ UNORM**
- **DXGI \_ 格式 \_ BC1 无格式 \_\\***
- **DXGI \_ FORMAT \_ BC1 \_ UNORM**
- **DXGI \_ FORMAT \_ BC1 \_ UNORM \_ SRGB**
- **DXGI \_ 格式 \_ BC2 无格式 \_\\***
- **DXGI \_ FORMAT \_ BC2 \_ UNORM**
- **DXGI \_ FORMAT \_ BC2 \_ UNORM \_ SRGB**
- **DXGI \_ 格式 \_ BC3 无格式 \_\\***
- **DXGI \_ FORMAT \_ BC3 \_ UNORM**
- **DXGI \_ FORMAT \_ BC3 \_ UNORM \_ SRGB**

此外，如果驱动程序在 Direct3D 功能级别9硬件上支持 Microsoft Direct3D 11 及更高版本，则这些驱动程序应支持 **DXGI \_ 格式 \_ L8 \_ UNORM** 占位符格式。 **DXGI \_格式 \_ L8 \_ UNORM** 在功能上等同于 **D3DDDIFMT \_ L8** 格式。

驱动程序还应支持 [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat) 枚举中的其他纹理格式：

-   **D3DDDIFMT \_ G8R8**
-   **D3DDDIFMT \_ R8**

 

