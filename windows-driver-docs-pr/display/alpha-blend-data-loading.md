---
title: Alpha 混合数据加载
description: Alpha 混合数据加载
ms.assetid: d61fbb07-a6b0-4623-bb5b-1c1218f570ae
keywords:
- alpha-blend 数据加载 WDK DirectX VA
- 混合图片 WDK DirectX VA，alpha-blend 数据加载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 820784ca57cc7cc98935251c971c06a22c9aec30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839071"
---
# <a name="alpha-blend-data-loading"></a>Alpha 混合数据加载


## <span id="ddk_alpha_blend_data_loading_gg"></span><span id="DDK_ALPHA_BLEND_DATA_LOADING_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)等于2时，指定的操作是加载数据，该数据用于指定与视频数据混合的 alpha 混合图面。 可以通过三种方式来加载 alpha 混合数据：

-   带有索引 alpha 4-4 （IA44）或 alpha 索引4-4 （AI44） alpha 混合图面的16项 AYUV 调色板

-   具有 DPXD、高光和 DCCMD 数据的16项 AYUV 调色板

-   AYUV 图面

[**DXVA\_ConfigAlphaLoad**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)结构确定使用哪些方法。

 

 





