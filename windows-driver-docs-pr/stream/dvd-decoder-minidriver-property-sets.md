---
title: DVD 解码器微型驱动程序属性集
description: DVD 解码器微型驱动程序属性集
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbdd6365171c6e5a858d2745451c9f8dbe635caa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795835"
---
# <a name="dvd-decoder-minidriver-property-sets"></a>DVD 解码器微型驱动程序属性集


## <span id="ddk_dvd_decoder_minidriver_property_sets_ks"></span><span id="DDK_DVD_DECODER_MINIDRIVER_PROPERTY_SETS_KS"></span>


本部分介绍 DVD 解码器特定的属性集，这些属性集可用于在 Microsoft Windows 98/Me、Windows 2000 和 Windows XP 及更高版本中使用 WDM 内核流式处理服务的 DVD 解码器微型驱动程序。

每个属性的引用页面都包含一个表，其中包含如下所示的列标题。


| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

这些标题具有以下含义：

-   **Get**

    目标 KS 对象是否支持 KSPROPERTY \_ 类型 \_ GET 属性请求？

-   **设置**

    目标 KS 对象是否支持 KSPROPERTY \_ 类型 \_ 集属性请求？

-   **Target**

    这是向其发送属性请求的 KS 对象。 DVD 解码器属性的目标是 "筛选器" 或 "pin"。  (属性请求按其内核句柄指定目标对象。 ) 

-   **属性描述符类型**

    属性说明符指定属性和要对该属性执行的操作。 描述符始终以 [**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 结构开始。

-   **属性值类型**

    属性具有值，并且此值的类型取决于属性。 例如，只能处于两种状态之一的属性（打开或关闭）通常具有布尔值。 可以假设从0到0xFFFFFFFF 的整数值的属性可能有 ULONG 值。 更复杂的属性可能具有作为数组或结构的值。

上面的属性说明符和属性值是在 [KS 属性、事件和方法](./ks-properties--events--and-methods.md)中讨论的实例规范和操作数据缓冲区的属性特定版本。

属性请求使用下列标志之一来指定要对属性执行的操作：

-   KSPROPERTY \_ 类型 \_ BASICSUPPORT

-   KSPROPERTY \_ 类型 \_ GET

-   KSPROPERTY \_ 类型 \_ 集

所有筛选器和 pin 对象均支持对其属性的基本支持操作。 它们是否支持 *get* 和 *Set* 操作取决于属性。 表示筛选器或固定对象的固有功能的属性可能只需要 get 操作。 尽管获取操作也可能对读取当前设置很有用，但表示可配置的设置的属性可能只需要设置操作。 有关使用 "获取"、"设置" 和 "使用 DVD 解码器的基本支持操作" 属性的详细信息，请参阅 [KS 属性](./ks-properties.md)。

属性查询或更改流方面。 几个属性集用于 DVD 解码器。 除了本主题中所述的属性集外，所有 DVD 解码器输入流还支持 DVD 版权保护属性集

每个属性说明都包含一个表，用于指示是否需要使用 DVD 解码器微型驱动程序来支持读取或写入属性。 \_对于微型驱动程序不支持的属性，DVD 解码器微型驱动程序应返回不 \_ 受支持的状态。

为 DVD 解码器微型驱动程序定义了以下属性集：

[KSPROPSETID \_ AudioDecoderOut](kspropsetid-audiodecoderout.md)

[KSPROPSETID \_ DvdSubPic](kspropsetid-dvdsubpic.md)

[KSPROPSETID \_ CopyProt](kspropsetid-copyprot.md)

[KSPROPSETID \_ TSRateChange](kspropsetid-tsratechange.md)

[KSPROPSETID \_ VPConfig 和 KSPROPSETID \_ VPVBIConfig](kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig.md)

[KSPROPSETID \_](kspropsetid-wave.md)

 

