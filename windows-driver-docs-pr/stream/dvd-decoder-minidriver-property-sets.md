---
title: DVD 解码器微型驱动程序属性集
description: DVD 解码器微型驱动程序属性集
ms.assetid: c24685bd-ea20-4cc2-b419-feb1fa2ea03e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 882c4fd988344d669d82f3338a19f81c10a801a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843220"
---
# <a name="dvd-decoder-minidriver-property-sets"></a>DVD 解码器微型驱动程序属性集


## <span id="ddk_dvd_decoder_minidriver_property_sets_ks"></span><span id="DDK_DVD_DECODER_MINIDRIVER_PROPERTY_SETS_KS"></span>


本部分介绍 DVD 解码器特定的属性集，这些属性集可用于在 Microsoft Windows 98/Me、Windows 2000 和 Windows XP 及更高版本中使用 WDM 内核流式处理服务的 DVD 解码器微型驱动程序。

每个属性的引用页面都包含一个表，其中包含如下所示的列标题。


| “获取” | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **获取**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_获取属性请求？

-   **字符集**

    目标 KS 对象是否支持 KSPROPERTY\_类型\_设置属性请求？

-   **靶**

    这是向其发送属性请求的 KS 对象。 DVD 解码器属性的目标是 "筛选器" 或 "pin"。 （属性请求按其内核句柄指定目标对象。）

-   **属性描述符类型**

    属性说明符指定属性和要对该属性执行的操作。 描述符始终以[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)结构开始。

-   **属性值类型**

    属性具有值，并且此值的类型取决于属性。 例如，只能处于两种状态之一的属性（打开或关闭）通常具有布尔值。 可以假设从0到0xFFFFFFFF 的整数值的属性可能有 ULONG 值。 更复杂的属性可能具有作为数组或结构的值。

上面的属性说明符和属性值是在[KS 属性、事件和方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)中讨论的实例规范和操作数据缓冲区的属性特定版本。

属性请求使用下列标志之一来指定要对属性执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_类型\_GET

-   KSPROPERTY\_类型\_集

所有筛选器和 pin 对象均支持对其属性的基本支持操作。 它们是否支持*get*和*Set*操作取决于属性。 表示筛选器或固定对象的固有功能的属性可能只需要 get 操作。 尽管获取操作也可能对读取当前设置很有用，但表示可配置的设置的属性可能只需要设置操作。 有关使用 "获取"、"设置" 和 "使用 DVD 解码器的基本支持操作" 属性的详细信息，请参阅[KS 属性](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)。

属性查询或更改流方面。 几个属性集用于 DVD 解码器。 除了本主题中所述的属性集外，所有 DVD 解码器输入流还支持 DVD 版权保护属性集

每个属性说明都包含一个表，用于指示是否需要使用 DVD 解码器微型驱动程序来支持读取或写入属性。 对于微型驱动程序不支持的属性的 get 或 set 请求，DVD 解码器微型驱动程序应返回\_不\_支持的状态。

为 DVD 解码器微型驱动程序定义了以下属性集：

[KSPROPSETID\_AudioDecoderOut](kspropsetid-audiodecoderout.md)

[KSPROPSETID\_DvdSubPic](kspropsetid-dvdsubpic.md)

[KSPROPSETID\_CopyProt](kspropsetid-copyprot.md)

[KSPROPSETID\_TSRateChange](kspropsetid-tsratechange.md)

[KSPROPSETID\_VPConfig 和 KSPROPSETID\_VPVBIConfig](kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig.md)

[KSPROPSETID\_波浪](kspropsetid-wave.md)

 

 





