---
title: 引脚数据范围和交集属性
description: 引脚数据范围和交集属性
keywords:
- 音频属性 WDK，pin
- WDM 音频属性 WDK，pin
- 锁定 WDK 音频，数据格式
- 数据范围格式 WDK 音频
- 格式化 WDK 音频、pin
- 与 WDK 音频交叉
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0923bebb53dec9fde95a7888922145bf601e3b3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800927"
---
# <a name="pin-data-range-and-intersection-properties"></a>引脚数据范围和交集属性


## <span id="pin_data_range_and_intersection_properties"></span><span id="PIN_DATA_RANGE_AND_INTERSECTION_PROPERTIES"></span>


几个属性请求提供有关音频流的数据格式的信息，音频流可以在其输入和输出插针处处理音频流。

Pin 支持的音频流数据格式在 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))派生结构的 [**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)数组中表示。 Pin 数据范围支持通过筛选器上的以下三个 [KSPROPSETID \_ Pin](../stream/kspropsetid-pin.md) 属性公开：

[**KSPROPERTY \_固定 \_ DATARANGES**](../stream/ksproperty-pin-dataranges.md) 此属性报告静态数据范围并表示支持的所有可能格式。 通常，数据范围包含在适配器驱动程序的静态数组中。
[**KSPROPERTY \_固定 \_ CONSTRAINEDDATARANGES**](../stream/ksproperty-pin-constraineddataranges.md) 此属性报告动态的数据范围，并表示属性请求时支持的格式子集。 属性处理程序应包含逻辑来确定 pin 在运行时能够支持的格式。 例如，硬件实现可能具有 DMA 约束，但在某些格式组合中不允许对全双工进行支持。
[**KSPROPERTY \_固定 \_ DATAINTERSECTION**](../stream/ksproperty-pin-dataintersection.md) 此属性从数据范围列表中选择一个数据格式。 选择基于动态功能，格式是从驱动程序在属性请求时可以支持的格式子集中获取的。 若要使用此属性，调用方提供数据范围的数组。 从第一个元素开始，属性处理程序搜索数组，直到找到当前能够支持的数据范围。 如果成功，处理程序将输出从该数据范围获取的数据格式并返回状态 \_ SUCCESS。 否则，处理程序返回状态 " \_ 无 \_ 匹配"。
音频系统组件使用 KSPROPERTY \_ pin \_ DATARANGES 和 KSPROPERTY \_ pin \_ DATAINTERSECTION 属性。 微型端口驱动程序应支持这些属性。 支持 KSPROPERTY \_ PIN \_ CONSTRAINEDDATARANGES 是可选的。

有关详细信息，请参阅 [音频数据格式和数据区域](audio-data-formats-and-data-ranges.md)。

**注意**  
KSPROPERTY \_ pin \_ DATARANGES 和 KSPROPERTY \_ pin \_ CONSTRAINEDDATARANGES 每个都是从一个8字节对齐地址开始。

 

 

