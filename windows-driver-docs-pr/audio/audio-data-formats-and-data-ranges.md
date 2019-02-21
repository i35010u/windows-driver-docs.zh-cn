---
title: 音频数据格式和数据区域
description: 音频数据格式和数据区域
ms.assetid: 85aa74b4-8e33-49f4-82e7-561baa55c265
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 413b512db5aa7b82e3acee7d71c5198bdfc6ef0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541903"
---
# <a name="audio-data-formats-and-data-ranges"></a>音频数据格式和数据区域


## <span id="audio_data_formats_and_data_ranges"></span><span id="AUDIO_DATA_FORMATS_AND_DATA_RANGES"></span>


音频驱动程序使用[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)并[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构，以指定音频流格式：

-   KS 数据流的数字格式指定开头 KSDATAFORMAT 结构 KS 格式说明符。

-   KS pin 可以支持的流格式的范围被指定由一系列 KS 数据范围;每个数组元素是一个范围说明符开头 KSDATARANGE 结构。

有关这些两个结构的详细信息，请参阅[KS 数据格式和数据范围](https://msdn.microsoft.com/library/windows/hardware/ff567632)。 有关 KS 数据范围的详细信息，请参阅[AVStream 中的数据范围交集](https://msdn.microsoft.com/library/windows/hardware/ff558680)。

本部分的其余部分将讨论以下主题：

[音频数据格式](audio-data-formats.md)

[音频数据范围](audio-data-ranges.md)

[可扩展的波形格式说明符](extensible-wave-format-descriptors.md)

[对于家庭影院系统的多渠道格式](multichannel-formats-for-home-theater-systems.md)

[音频数据格式和数据区域的示例](examples-of-audio-data-formats-and-data-ranges.md)

 

 




