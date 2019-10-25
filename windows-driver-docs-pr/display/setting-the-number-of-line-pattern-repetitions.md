---
title: 设置线条模式重复次数
description: 设置线条模式重复次数
ms.assetid: 090b823a-59d0-40e1-8feb-0b03b7f08fee
keywords:
- 线路模式重复 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8baddb7079866688acfb3f8a7be1a8492bc9b7c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825812"
---
# <a name="setting-the-number-of-line-pattern-repetitions"></a>设置线条模式重复次数


## <span id="ddk_setting_the_number_of_line_pattern_repetitions_gg"></span><span id="DDK_SETTING_THE_NUMBER_OF_LINE_PATTERN_REPETITIONS_GG"></span>


应用程序可以指导 Direct3D 设备使用实线或带图案的线条呈现基元。 如果设备支持重复模式，应用程序还可以拉伸特定的线条模式。 设备的驱动程序必须将 D3DPMISCCAPS\_LINEPATTERNREP 标志设置为指示设备支持重复特定线路模式。 设置此标志的方式取决于 DirectX 版本：

-   对于 DirectX 7.0 和更早版本，请在[**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构的**dwMiscCaps**成员中设置此标志。

-   对于 DirectX 8.0 和更高版本，请在 D3DCAPS*Xx*结构的**PrimitiveMiscCaps**成员中设置此标志，其中*xx*表示 DirectX 版本（例如，版本8的 D3DCAPS8，版本9的 D3DCAPS9）。 D3DCAPS8 和 D3DCAPS9 在其各自版本的 DirectX SDK 文档中进行了介绍。

当应用程序为 D3DRENDERSTATE\_LINEPATTERN （或 D3DRS\_LINEPATTERN）呈现状态设置呈现状态值时，它们可以通过设置的**wRepeatFactor**成员来指定重复行模式的次数。D3DLINEPATTERN 结构。 应用程序可将此成员的最大值设置为65535（16位值）。 但是，硬件仅支持最大为255（8位值）。 因此，显示驱动程序必须将尝试将行模式重复数字设置为大于255的值的请求失败，因为该请求无效。 DirectX SDK 文档中介绍了 D3DLINEPATTERN。

 

 





