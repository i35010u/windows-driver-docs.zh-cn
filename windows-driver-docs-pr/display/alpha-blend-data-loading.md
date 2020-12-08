---
title: Alpha 混合数据加载
description: Alpha 混合数据加载
keywords:
- alpha-blend 数据加载 WDK DirectX VA
- 混合图片 WDK DirectX VA，alpha-blend 数据加载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 967f305fdeb22688c3dd744328e6a3ffb792af31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810493"
---
# <a name="alpha-blend-data-loading"></a>Alpha 混合数据加载


## <span id="ddk_alpha_blend_data_loading_gg"></span><span id="DDK_ALPHA_BLEND_DATA_LOADING_GG"></span>


当 [bDXVA \_ Func 变量](bdxva-func-variable.md) 等于2时，指定的操作是加载数据，该数据用于指定与视频数据混合的 alpha 混合图面。 可以通过三种方式来加载 alpha 混合数据：

-   16 entry AYUV 调色板，其索引为 4-4 (IA44) 或 alpha 索引 4-4 (AI44) alpha 混合图面

-   具有 DPXD、高光和 DCCMD 数据的16项 AYUV 调色板

-   AYUV 图面

[**DXVA \_ ConfigAlphaLoad**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)结构确定使用哪些方法。

 

