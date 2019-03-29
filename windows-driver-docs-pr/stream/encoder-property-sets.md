---
title: 编码器属性集
description: 编码器属性集
ms.assetid: b273464d-0d40-488c-a848-291f949609f0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ed4485ba5eec89b0939ee305284bb271f57dc2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568143"
---
# <a name="encoder-property-sets"></a>编码器属性集


## <span id="ddk_encoder_property_sets_ks"></span><span id="DDK_ENCODER_PROPERTY_SETS_KS"></span>


本部分介绍的编码器和可用于在 Microsoft Windows 98 中使用 WDM 内核流式处理服务的编码器微型驱动程序的编解码器特定于 API 的属性集 / Me、 Windows 2000 和 Windows XP 及更高版本。

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

    这是请求发送到哪个属性 KS 对象。 视频编码器属性的目标是筛选器或 pin。 （属性请求指定的目标对象由其内核句柄。）

-   **属性描述符类型**

    属性描述符指定的属性和要在该属性上执行的操作。 描述符始终开头[ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)结构。

-   **属性值类型**

    属性的值，而此值的类型取决于属性。 例如，可以是一个只有两种状态-打开或关闭-中的属性通常具有一个 BOOL 值。 可以假定为 0xFFFFFFFF 0x0 从整数值的属性可能具有 ULONG 值。 更复杂的属性可能是数组或结构的值。

属性描述符和更高版本的属性值是实例规范和操作数据缓冲区中所述的属性特定于版本[KS 属性、 事件和方法](https://msdn.microsoft.com/library/windows/hardware/ff567673)。

属性请求使用下列标志之一来指定要在属性上执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_TYPE\_GET

-   KSPROPERTY\_TYPE\_SET

所有筛选器和 pin 对象支持属性对其的 basic 支持操作。 是否支持*获取*并*设置*操作取决于属性。 该属性表示的筛选器或 pin 对象的固有功能是可能需要仅*获取*操作。 表示可配置的设置的属性可能只需要*设置*操作，尽管*获取*操作也可能适用于读取的当前设置。 有关使用具有视频编码器属性的 get、 集和 basic 支持操作的详细信息，请参阅[KS 属性](https://msdn.microsoft.com/library/windows/hardware/ff567671)。

每个属性的说明中的表指示是否需要视频编码器微型驱动程序以支持读取或写入属性。 视频编码器微型驱动程序应返回状态\_不\_要获取或设置为不受微型驱动程序的属性的请求的响应中受支持。

以下属性集每个包含一个视频编码器微型驱动程序必须实现的属性。 即，有效地每个属性获取自己的一组，因此指定 0 **PropertyId**的成员[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176) 中的成员[ **KSPROPERTY\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff565617)结构，根据需要。

下面的属性设置属于编解码器 API:

[CODECAPI\_VIDEO\_ENCODER](codecapi-video-encoder.md)

[CODECAPI\_AUDIO\_ENCODER](codecapi-audio-encoder.md)

[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)

[CODECAPI\_SUPPORTSEVENTS](codecapi-supportsevents.md)

[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)

下面的属性设置属于编码器 API:

[ENCAPIPARAM\_BITRATE](encapiparam-bitrate.md)

[ENCAPIPARAM\_BITRATE\_MODE](encapiparam-bitrate-mode.md)

[ENCAPIPARAM\_PEAK\_BITRATE](encapiparam-peak-bitrate.md)

 

 





