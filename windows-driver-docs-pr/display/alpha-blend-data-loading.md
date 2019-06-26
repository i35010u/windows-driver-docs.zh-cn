---
title: Alpha 混合数据加载
description: Alpha 混合数据加载
ms.assetid: d61fbb07-a6b0-4623-bb5b-1c1218f570ae
keywords:
- alpha 混合数据加载 WDK DirectX VA
- 混合型的图片 WDK DirectX VA，alpha 混合数据加载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fccf18e298e57e79a4027f5503247d3c719e3489
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384637"
---
# <a name="alpha-blend-data-loading"></a>Alpha 混合数据加载


## <span id="ddk_alpha_blend_data_loading_gg"></span><span id="DDK_ALPHA_BLEND_DATA_LOADING_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)是等于 2，指定的操作是加载指定的 alpha 值混合处理图面以与视频数据混合的数据。 有三种方法可以加载的 alpha 值混合处理数据：

-   16 项 AYUV 调色板其索引的 alpha 4-4 (IA44) 或 alpha 索引 4-4 (AI44) alpha 值混合处理图面

-   16 项 AYUV 调色板 DPXD、 突出显示和 DCCMD 数据

-   AYUV 图形图面

[ **DXVA\_ConfigAlphaLoad** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configalphaload)结构确定哪种方法使用。

 

 





