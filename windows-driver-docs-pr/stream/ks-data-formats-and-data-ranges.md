---
title: KS 数据格式和数据范围
description: KS 数据格式和数据范围
ms.assetid: 44b55a5a-ec58-4c1e-b780-e20829fe3edf
keywords:
- 流式处理数据格式 WDK 内核
- 流式处理格式 WDK 内核
- 流式处理的范围 WDK 内核
- 流式处理的数据范围 WDK 内核
- KS 数据格式以 WDK 内核流式处理
- KS 数据范围 WDK 内核流式处理
- KSDATARANGE
- KSDATAFORMAT
- 流式处理 WDK，数据范围的内核
- KS WDK，数据范围
- 流式处理 WDK，数据格式的内核
- KS WDK，数据格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 298a08b7027ea3a9a53698390d7a1563a67a9c49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382520"
---
# <a name="ks-data-formats-and-data-ranges"></a>KS 数据格式和数据范围





KS 插针指定数据格式和范围使用[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)并[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构。 数据格式指定数据流，例如音频采样大小为 16 位的单个属性。 数据范围指定多种格式，例如音频采样 16 至 24 位的范围。

微型驱动程序包含一个 KSDATARANGE 结构的数组中每个[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)它提供的结构。 Microsoft 提供的格式中枚举*ksmedia.h*。

KSDATARANGE 结构具有相同的成员作为 KSDATAFORMAT 结构;但是，微型驱动程序可以为 KSDATARANGE 的主要格式、 子格式，以及说明符成员指定通配符值。

微型驱动程序使用这些结构的扩展的版本来定义特定于媒体的值。 若要了解此音频和视频捕获中的工作方式，请参阅：[音频数据格式和数据范围](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-data-formats-and-data-ranges)并[选择 Stream 格式](selecting-a-stream-format.md)。

客户端使用的 pin 由筛选器上的给定的 pin 工厂实例化查询的数据格式支持以下属性：

-   [**KSPROPERTY\_PIN\_DATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)。 KS 筛选器将报告所有支持的 pin，pin 工厂实例化的数据范围。 这包括 pin 可以每种数据格式*曾经*支持。

-   [**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)。 KS 筛选器报告受 pin 实例化 pin 工厂，根据当前的内部驱动程序状态的所有数据范围。

-   [**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)。 如果通过 pin 工厂实例化的 pin 支持特定的数据格式，客户端可以使用此属性设置为查询。

-   [**KSPROPERTY\_PIN\_DATAINTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)。 客户端可以使用此属性提供广泛的数据格式。

Pin 实例化后，用户模式下客户端可以确定当前的数据格式或请求的数据格式通过更改[KSPROPSETID\_连接](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-connection)属性请求。 例如，使用客户端[ **KSPROPERTY\_连接\_PROPOSEDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-proposedataformat)若要确定 pin 是否支持给定的数据格式。 客户端使用[ **KSPROPERTY\_连接\_DATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-dataformat)若要更改的数据格式。

KS 微型驱动程序和客户端可以动态协商数据格式。 当流的数据格式更改时，微型驱动程序指定 KSSTREAM\_标头\_OPTIONSF\_DATADISCONTINUITY 标志**OptionsFlags** KSSTREAM 成员\_标头。 微型驱动程序将传递的新数据格式本身中所述[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)结构，请在相应的数据缓冲区。

 

 




