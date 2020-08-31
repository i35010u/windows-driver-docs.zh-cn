---
title: 设置线条模式重复次数
description: 设置线条模式重复次数
ms.assetid: 090b823a-59d0-40e1-8feb-0b03b7f08fee
keywords:
- 线路模式重复 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c91988f3ac682bf4c69bcd65862fbc8d7f70abf4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063466"
---
# <a name="setting-the-number-of-line-pattern-repetitions"></a>设置线条模式重复次数


## <span id="ddk_setting_the_number_of_line_pattern_repetitions_gg"></span><span id="DDK_SETTING_THE_NUMBER_OF_LINE_PATTERN_REPETITIONS_GG"></span>


应用程序可以指导 Direct3D 设备使用实线或带图案的线条呈现基元。 如果设备支持重复模式，应用程序还可以拉伸特定的线条模式。 设备的驱动程序必须设置 D3DPMISCCAPS \_ LINEPATTERNREP 标志，以指示设备支持重复特定线路模式。 设置此标志的方式取决于 DirectX 版本：

-   对于 DirectX 7.0 和更早版本，请在[**D3DPRIMCAPS**](/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwMiscCaps**成员中设置此标志。

-   对于 DirectX 8.0 和更高版本，请在 D3DCAPS*Xx*结构的**PrimitiveMiscCaps**成员中设置此标志，其中*xx*表示 DirectX 版本 (例如，D3DCAPS8 用于版本8，版本 9) 。 D3DCAPS8 和 D3DCAPS9 在其各自版本的 DirectX SDK 文档中进行了介绍。

当应用程序为 D3DRENDERSTATE \_ LINEPATTERN (或 D3DRS LINEPATTERN) render 状态设置呈现状态值时 \_ ，它们可以通过设置 wRepeatFactor 结构的 **D3DLINEPATTERN** 成员来指定重复行模式的次数。 应用程序可将此成员设置为 65535 (16 位值) 的最大值。 但是，硬件仅支持最大为 255 (8 位值) 。 因此，显示驱动程序必须将尝试将行模式重复数字设置为大于255的值的请求失败，因为该请求无效。 DirectX SDK 文档中介绍了 D3DLINEPATTERN。

 

