---
title: 设置线条模式重复次数
description: 设置线条模式重复次数
ms.assetid: 090b823a-59d0-40e1-8feb-0b03b7f08fee
keywords:
- 行模式重复 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e613c3ac27101017036c2842fbd42cff1d2c548
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365550"
---
# <a name="setting-the-number-of-line-pattern-repetitions"></a>设置线条模式重复次数


## <span id="ddk_setting_the_number_of_line_pattern_repetitions_gg"></span><span id="DDK_SETTING_THE_NUMBER_OF_LINE_PATTERN_REPETITIONS_GG"></span>


应用程序可以直接呈现基元使用纯色或图案的线条的 Direct3D 设备。 如果设备支持重复模式，应用程序也可以延迟特定行模式。 设备的驱动程序必须设置 D3DPMISCCAPS\_LINEPATTERNREP 标志以指示设备是否支持重复的特定行模式。 如何设置此标志取决于 DirectX 版本：

-   对于 DirectX 7.0 及更早版本，在中设置此标志**dwMiscCaps**的成员[ **D3DPRIMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dcaps/ns-d3dcaps-_d3dprimcaps)结构。

-   DirectX 8.0 及更高版本，在中设置此标志**PrimitiveMiscCaps** D3DCAPS 成员*Xx*结构，其中*Xx*指示 DirectX 版本 (例如，D3DCAPS8版本 8 和 D3DCAPS9 版本 9）。 D3DCAPS8 和 D3DCAPS9 及其各自的版本的 DirectX SDK 文档中所述。

当应用程序呈现状态将的值设置 D3DRENDERSTATE\_LINEPATTERN (或 D3DRS\_LINEPATTERN) 呈现状态，他们可以指定的次数重复行模式通过设置**wRepeatFactor** D3DLINEPATTERN 结构中的成员。 应用程序可以将此成员设置为最大值 65535 （16 位值）。 但是，硬件仅支持最多为 255 （8 位值）。 因此，显示器驱动程序必须失败的请求，尝试设置一个值为行模式重复数大于 255 为无效的请求。 D3DLINEPATTERN 是 DirectX SDK 文档中所述。

 

 





