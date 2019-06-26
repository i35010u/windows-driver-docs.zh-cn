---
title: DirectX 8.0 DDI 最低支持要求
description: DirectX 8.0 DDI 最低支持要求
ms.assetid: 8758e25e-e54f-42e5-a23d-354af634bce9
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，最小支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 875829941427fac96afdf08901be3c490036d1fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385600"
---
# <a name="minimal-directx-80-ddi-support"></a>DirectX 8.0 DDI 最低支持要求


## <span id="ddk_minimal_directx_8_0_ddi_support_gg"></span><span id="DDK_MINIMAL_DIRECTX_8_0_DDI_SUPPORT_GG"></span>


DirectX 8.0 DirectX 7.0 级别驱动程序通过提供硬件加速。 但是，对于公开任何 DirectX 8.0 的新功能，如多个顶点流、 索引缓冲区或顶点和像素着色器的驱动程序，它必须通过报告 DirectX 8.0 样式功能将自身标识并支持新[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)呈现令牌。 为了支持新 D3dDrawPrimitives2 呈现该驱动程序的令牌，才能为顶点流和固定的函数顶点着色器提供基本支持。

报告 DirectX 8.0 样式功能包括以下步骤：

-   处理新**GetDriverInfo2**变体的现有[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)入口点。

-   返回一个包含设备请求时的功能的 D3DCAPS8 结构。

-   确保该结构定义的字段具有某些最小值。

-   返回纹理格式列表，其中包括 DirectX 8.0 样式图面格式说明。

这些各种要求以下各节所述。

 

 





