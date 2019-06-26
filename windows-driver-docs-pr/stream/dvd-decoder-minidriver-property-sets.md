---
title: DVD 解码器微型驱动程序属性集
description: DVD 解码器微型驱动程序属性集
ms.assetid: c24685bd-ea20-4cc2-b419-feb1fa2ea03e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0296cc1724e547ef9039ae925860a7663ae159c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358427"
---
# <a name="dvd-decoder-minidriver-property-sets"></a>DVD 解码器微型驱动程序属性集


## <span id="ddk_dvd_decoder_minidriver_property_sets_ks"></span><span id="DDK_DVD_DECODER_MINIDRIVER_PROPERTY_SETS_KS"></span>


本部分介绍可用于在 Microsoft Windows 98 中使用 WDM 内核流式处理服务的 DVD 解码器微型的 DVD 解码器特定的属性集 / Me、 Windows 2000 和 Windows XP 及更高版本。

每个属性的参考页包含具有如下所示的列标题的表。


| Get | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **Get**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_属性的 GET 请求？

-   **Set**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_集属性请求？

-   **Target**

    这是请求发送到哪个属性 KS 对象。 DVD 解码器属性的目标是筛选器或 pin。 （属性请求指定的目标对象由其内核句柄。）

-   **属性描述符类型**

    属性描述符指定的属性和要在该属性上执行的操作。 描述符始终开头[ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)结构。

-   **属性值类型**

    属性的值，而此值的类型取决于属性。 例如，可以是一个只有两种状态-打开或关闭-中的属性通常具有一个布尔值。 可以假定为 0xFFFFFFFF 0 的整数值的属性可能具有 ULONG 值。 更复杂的属性可能是数组或结构的值。

属性描述符和更高版本的属性值是实例规范和操作数据缓冲区中所述的属性特定于版本[KS 属性、 事件和方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)。

属性请求使用下列标志之一来指定要在属性上执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_TYPE\_GET

-   KSPROPERTY\_TYPE\_SET

所有筛选器和 pin 对象支持属性对其的 basic 支持操作。 是否支持*获取*并*设置*操作取决于属性。 该属性表示的筛选器或 pin 对象的固有功能是可能需要仅一个 get 操作。 该属性表示可配置的设置可能需要仅设置操作中，尽管可能适用于读取的当前设置的 get 操作。 有关使用 DVD 解码器属性中使用 get、 集和 basic 支持操作的详细信息，请参阅[KS 属性](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)。

查询或更改流方面的属性。 多个属性集用于 DVD 解码器。 所有的 DVD 解码器输入的流支持除了设置为本主题中所述的属性集的 DVD 版权保护属性

每个属性描述包含一个数据表，说明是否需要 DVD 解码器微型驱动程序来支持读取或写入属性。 DVD 解码器微型驱动程序应返回状态\_不\_要获取或设置为不受微型驱动程序的属性的请求的响应中受支持。

下面的属性设置为 DVD 解码器微型驱动程序定义：

[KSPROPSETID\_AudioDecoderOut](kspropsetid-audiodecoderout.md)

[KSPROPSETID\_DvdSubPic](kspropsetid-dvdsubpic.md)

[KSPROPSETID\_CopyProt](kspropsetid-copyprot.md)

[KSPROPSETID\_TSRateChange](kspropsetid-tsratechange.md)

[KSPROPSETID\_VPConfig 和 KSPROPSETID\_VPVBIConfig](kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig.md)

[KSPROPSETID\_Wave](kspropsetid-wave.md)

 

 





