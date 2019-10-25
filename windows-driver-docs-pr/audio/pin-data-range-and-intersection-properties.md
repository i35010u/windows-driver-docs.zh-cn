---
title: 引脚数据范围和交集属性
description: 引脚数据范围和交集属性
ms.assetid: 55a749b2-1f54-42f8-876c-f391112d7bab
keywords:
- 音频属性 WDK，pin
- WDM 音频属性 WDK，pin
- 锁定 WDK 音频，数据格式
- 数据范围格式 WDK 音频
- 格式化 WDK 音频、pin
- 与 WDK 音频交叉
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 491cc55f5b49a878765ffc80f120826d2ae8030a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832502"
---
# <a name="pin-data-range-and-intersection-properties"></a>引脚数据范围和交集属性


## <span id="pin_data_range_and_intersection_properties"></span><span id="PIN_DATA_RANGE_AND_INTERSECTION_PROPERTIES"></span>


几个属性请求提供有关音频流的数据格式的信息，音频流可以在其输入和输出插针处处理音频流。

Pin 支持的音频流数据格式在[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))派生结构的[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)数组中表示。 Pin 数据范围支持通过以下三个[KSPROPSETID\_](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)在筛选器上固定属性：

[**KSPROPERTY\_PIN\_DATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)此属性报告静态数据范围并表示支持的所有可能格式。 通常，数据范围包含在适配器驱动程序的静态数组中。
[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)此属性报告动态的数据范围，并表示属性请求时支持的格式子集。 属性处理程序应包含逻辑来确定 pin 在运行时能够支持的格式。 例如，硬件实现可能具有 DMA 约束，但在某些格式组合中不允许对全双工进行支持。
[**KSPROPERTY\_PIN\_DATAINTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)此属性从数据范围列表中选择一个数据格式。 选择基于动态功能，格式是从驱动程序在属性请求时可以支持的格式子集中获取的。 若要使用此属性，调用方提供数据范围的数组。 从第一个元素开始，属性处理程序搜索数组，直到找到当前能够支持的数据范围。 如果成功，处理程序将输出从该数据范围获取的数据格式，并返回状态\_SUCCESS。 否则，处理程序返回状态\_没有\_匹配。
音频系统组件使用 KSPROPERTY\_PIN\_DATARANGES 和 KSPROPERTY\_PIN\_DATAINTERSECTION 属性。 微型端口驱动程序应支持这些属性。 支持 KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES 是可选的。

有关详细信息，请参阅[音频数据格式和数据区域](audio-data-formats-and-data-ranges.md)。

**请注意**   KSPROPERTY\_固定\_DATARANGES 和 KSPROPERTY\_PIN\_每个从8字节对齐的地址开始。

 

 

 




