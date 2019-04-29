---
title: DirectX 8.0 DDI 最低支持要求
description: DirectX 8.0 DDI 最低支持要求
ms.assetid: 8758e25e-e54f-42e5-a23d-354af634bce9
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，最小支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f58ac91933e961a3d3c46adddd2841a35097d7c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390820"
---
# <a name="minimal-directx-80-ddi-support"></a>DirectX 8.0 DDI 最低支持要求


## <span id="ddk_minimal_directx_8_0_ddi_support_gg"></span><span id="DDK_MINIMAL_DIRECTX_8_0_DDI_SUPPORT_GG"></span>


DirectX 8.0 DirectX 7.0 级别驱动程序通过提供硬件加速。 但是，对于公开任何 DirectX 8.0 的新功能，如多个顶点流、 索引缓冲区或顶点和像素着色器的驱动程序，它必须通过报告 DirectX 8.0 样式功能将自身标识并支持新[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)呈现令牌。 为了支持新 D3dDrawPrimitives2 呈现该驱动程序的令牌，才能为顶点流和固定的函数顶点着色器提供基本支持。

报告 DirectX 8.0 样式功能包括以下步骤：

-   处理新**GetDriverInfo2**变体的现有[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)入口点。

-   返回一个包含设备请求时的功能的 D3DCAPS8 结构。

-   确保该结构定义的字段具有某些最小值。

-   返回纹理格式列表，其中包括 DirectX 8.0 样式图面格式说明。

这些各种要求以下各节所述。

 

 





