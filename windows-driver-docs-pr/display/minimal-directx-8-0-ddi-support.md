---
title: DirectX 8.0 DDI 最低支持要求
description: DirectX 8.0 DDI 最低支持要求
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，最小支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47a56beb2d028c6c9e442a670e53d179ece49e3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822472"
---
# <a name="minimal-directx-80-ddi-support"></a>DirectX 8.0 DDI 最低支持要求


## <span id="ddk_minimal_directx_8_0_ddi_support_gg"></span><span id="DDK_MINIMAL_DIRECTX_8_0_DDI_SUPPORT_GG"></span>


DirectX 8.0 通过 DirectX 7.0 级别驱动程序提供硬件加速。 但是，若要使驱动程序公开 DirectX 8.0 的任何新功能（例如多个顶点流、索引缓冲区或顶点和像素着色器），则它必须通过报告 DirectX 8.0 样式功能并支持新的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 呈现令牌来自行标识。 为了支持新的 D3dDrawPrimitives2 呈现标记，驱动程序需要提供对顶点流和固定函数顶点着色器的基本支持。

报告 DirectX 8.0 样式功能涉及以下步骤：

-   处理现有 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)入口点的新 **GetDriverInfo2** 变体。

-   在请求时返回包含设备功能的 D3DCAPS8 结构。

-   确保该结构的已定义字段具有某些最小值。

-   返回包含 DirectX 8.0 样式表面格式说明的纹理格式列表。

以下各节将讨论这些不同的要求。

 

