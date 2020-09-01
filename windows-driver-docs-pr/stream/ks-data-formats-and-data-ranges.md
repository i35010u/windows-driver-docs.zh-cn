---
title: KS 数据格式和数据范围
description: KS 数据格式和数据范围
ms.assetid: 44b55a5a-ec58-4c1e-b780-e20829fe3edf
keywords:
- 数据格式 WDK 内核流式处理
- 格式化 WDK 内核流式处理
- 范围 WDK 内核流式处理
- 数据范围 WDK 内核流式处理
- KS 数据格式 WDK 内核流式处理
- KS 数据范围 WDK 内核流式处理
- KSDATARANGE
- KSDATAFORMAT
- 内核流 WDK，数据范围
- KS WDK，数据范围
- 内核流 WDK，数据格式
- KS WDK，数据格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69279c70dfc75e47a071677b2395a2e37f95cf7b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186629"
---
# <a name="ks-data-formats-and-data-ranges"></a>KS 数据格式和数据范围





KS 引脚使用 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 和 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构指定数据格式和范围。 数据格式指定数据流的单个属性，例如16位的音频采样大小。 数据范围指定多种格式，例如，16-24 位的音频采样范围。

微型驱动程序在它提供的每个 [**KSPIN \_ 说明符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor) 结构中包含一组 KSDATARANGE 结构。 在 *ksmedia*中枚举 Microsoft 提供的格式。

KSDATARANGE 结构具有与 KSDATAFORMAT 结构相同的成员;但是，微型驱动程序可以为 KSDATARANGE 的主要格式、subformat 和说明符成员指定通配符值。

微型驱动程序使用这些结构的扩展版本来定义特定于媒体的值。 若要了解此功能在音频和视频捕获中的工作原理，请参阅： [音频数据格式和数据范围](../audio/audio-data-formats-and-data-ranges.md) 和 [选择流格式](selecting-a-stream-format.md)。

客户端使用以下属性来查询对由筛选器上给定的 pin 工厂实例化的 pin 的数据格式支持：

-   [**KSPROPERTY \_固定 \_ DATARANGES**](./ksproperty-pin-dataranges.md)。 KS 筛选器报告由 pin 工厂实例化的 pin 支持的所有数据范围。 这包括 *pin 可以支持* 的每个数据格式。

-   [**KSPROPERTY \_固定 \_ CONSTRAINEDDATARANGES**](./ksproperty-pin-constraineddataranges.md)。 如果当前的内部驱动程序状态为，则 KS 筛选器将报告由 pin 工厂实例化的 pin 支持的所有数据范围。

-   [**KSPROPERTY \_固定 \_ PROPOSEDATAFORMAT**](./ksproperty-pin-proposedataformat.md)。 客户端可以使用此属性来查询 pin 工厂实例化的 pin 是否支持特定的数据格式。

-   [**KSPROPERTY \_固定 \_ DATAINTERSECTION**](./ksproperty-pin-dataintersection.md)。 客户端可以使用此属性提供一系列数据格式。

在实例化 pin 后，用户模式客户端可以通过 [KSPROPSETID \_ 连接](./kspropsetid-connection.md) 属性请求来确定当前数据格式或请求更改数据格式。 例如，客户端使用 [**KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT**](./ksproperty-connection-proposedataformat.md) 来确定 pin 是否支持给定的数据格式。 客户端使用 [**KSPROPERTY \_ 连接 \_ DATAFORMAT**](./ksproperty-connection-dataformat.md) 来更改数据格式。

KS 微型驱动程序和客户端可以动态协商数据格式。 当流的数据格式更改时，微型驱动程序在 \_ \_ \_ OptionsFlags 标头的 **KSSTREAM** 成员中指定 KSSTREAM 标头 OPTIONSF DATADISCONTINUITY 标志 \_ 。 微型驱动程序在相应的数据缓冲区中传递 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 结构中所述的新数据格式。

 

