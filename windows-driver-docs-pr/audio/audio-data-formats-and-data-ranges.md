---
title: 音频数据格式和数据范围
description: 音频数据格式和数据范围
ms.assetid: 85aa74b4-8e33-49f4-82e7-561baa55c265
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a94c4280925bfac0b147ae15495dc3869701a9b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208359"
---
# <a name="audio-data-formats-and-data-ranges"></a>音频数据格式和数据范围


## <span id="audio_data_formats_and_data_ranges"></span><span id="AUDIO_DATA_FORMATS_AND_DATA_RANGES"></span>


音频驱动程序使用 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 和 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构来指定音频流格式：

-   KS 数据流的数字格式由以 KSDATAFORMAT 结构开头的 KS 格式说明符指定。

-   KS pin 可以支持的流格式范围由 KS 数据范围的数组指定;每个数组元素都是一个以 KSDATARANGE 结构开头的范围说明符。

有关这两个结构的详细信息，请参阅 [KS 数据格式和数据区域](../stream/ks-data-formats-and-data-ranges.md)。 有关 KS 数据范围的详细信息，请参阅 [AVStream 中的数据范围交集](../stream/data-range-intersections-in-avstream.md)。

本部分的其余部分将讨论以下主题：

[音频数据格式](audio-data-formats.md)

[音频数据范围](audio-data-ranges.md)

[可扩展的波形格式描述符](extensible-wave-format-descriptors.md)

[适用于家庭影院系统的多声道格式](multichannel-formats-for-home-theater-systems.md)

[音频数据格式和数据范围的示例](examples-of-audio-data-formats-and-data-ranges.md)

 

