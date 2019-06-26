---
title: 引脚数据范围和交集属性
description: 引脚数据范围和交集属性
ms.assetid: 55a749b2-1f54-42f8-876c-f391112d7bab
keywords:
- 音频属性 WDK，pin
- WDM 音频属性 WDK，pin
- pin WDK 音频数据格式
- 数据范围格式 WDK 音频
- 格式 WDK 音频 pin
- 交集 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5914c94adc546c08ddd5fd82b67a2e7ab027b30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355305"
---
# <a name="pin-data-range-and-intersection-properties"></a>引脚数据范围和交集属性


## <span id="pin_data_range_and_intersection_properties"></span><span id="PIN_DATA_RANGE_AND_INTERSECTION_PROPERTIES"></span>


多个属性请求提供音频设备是能够在其输入和输出插针，处理音频流的数据格式的信息。

用表示 pin 是否能够支持的音频流数据格式[ **KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)数组[ **KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))-派生结构。 通过以下三种公开 pin 数据范围的支持[KSPROPSETID\_Pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)上筛选器的属性：

[**KSPROPERTY\_PIN\_DATARANGES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)此属性报告是静态的表示所有可能的格式支持的数据范围。 通常情况下，数据区域包含在适配器驱动程序中的静态数组中。
[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)此属性报告是动态的表示支持在属性请求的时间格式的子集的数据范围。 属性处理程序应包含的逻辑来决定哪些格式 pin 能够在运行时支持。 例如，硬件实现可能具有某些格式组合中不允许使用支持全双工 DMA 约束。
[**KSPROPERTY\_PIN\_DATAINTERSECTION** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)此属性从数据区域的列表中选择一种数据格式。 上的动态功能基于所选内容和格式中获取该驱动程序可以支持属性请求时的格式的子集。 若要使用此属性，而调用方提供一的系列数据范围。 从开始的第一个元素，属性处理程序搜索的数组的操作，直到它找到的数据范围是当前能够支持。 如果成功，该处理程序将输出数据格式，则来自该数据区域，并返回状态\_成功。 否则，该处理程序将返回状态\_否\_匹配项。
音频系统组件使用 KSPROPERTY\_PIN\_DATARANGES 和 KSPROPERTY\_PIN\_DATAINTERSECTION 属性。 微型端口驱动程序应支持这些属性。 支持 KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES 是可选的。

有关详细信息，请参阅[音频数据格式和数据范围](audio-data-formats-and-data-ranges.md)。

**请注意**   KSPROPERTY\_PIN\_DATARANGES 和 KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES 每个 8 字节对齐地址上开始。

 

 

 




