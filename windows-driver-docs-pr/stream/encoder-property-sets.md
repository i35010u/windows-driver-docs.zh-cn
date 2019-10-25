---
title: 编码器属性集
description: 编码器属性集
ms.assetid: b273464d-0d40-488c-a848-291f949609f0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30889d8645ee09aa3be784218f2cb71ab9851c54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834428"
---
# <a name="encoder-property-sets"></a>编码器属性集


## <span id="ddk_encoder_property_sets_ks"></span><span id="DDK_ENCODER_PROPERTY_SETS_KS"></span>


本部分介绍了编码器和编解码器 API 特定的属性集，这些属性集可用于在 Microsoft Windows 98/Me、Windows 2000 和 Windows XP 及更高版本中使用 WDM 内核流式处理服务的编码器微型驱动程序。

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

    这是向其发送属性请求的 KS 对象。 视频编码器属性的目标是筛选器或 pin。 （属性请求按其内核句柄指定目标对象。）

-   **属性描述符类型**

    属性说明符指定属性和要对该属性执行的操作。 描述符始终以[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)结构开始。

-   **属性值类型**

    属性具有值，并且此值的类型取决于属性。 例如，一个只能处于两种状态的属性（打开或关闭）通常具有 BOOL 值。 可以假设从0x0 到0xFFFFFFFF 的整数值的属性可能具有 ULONG 值。 更复杂的属性可能具有作为数组或结构的值。

上面的属性说明符和属性值是在[KS 属性、事件和方法](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)中讨论的实例规范和操作数据缓冲区的属性特定版本。

属性请求使用下列标志之一来指定要对属性执行的操作：

-   KSPROPERTY\_类型\_BASICSUPPORT

-   KSPROPERTY\_类型\_GET

-   KSPROPERTY\_类型\_集

所有筛选器和 pin 对象均支持对其属性的基本支持操作。 它们是否支持*get*和*Set*操作取决于属性。 表示筛选器或固定对象的固有功能的属性可能只需要*get*操作。 尽管*获取*操作也可能对读取当前设置很有用，但表示可配置的设置的属性可能只需要*设置*操作。 若要详细了解如何使用带有视频编码器属性的 get、set 和 basic 支持操作，请参阅[KS properties](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)。

每个属性的说明中的表指示是否需要视频编码器微型驱动程序来支持读取或写入属性。 视频编码器微型驱动程序应返回\_不\_支持的状态，以响应对微型驱动程序不支持的属性的 get 或 set 请求。

下面的每个属性集都包含一个属性，该属性必须由视频编码器微型驱动程序实现。 这就是，实际上每个属性都获取自己的集，因此请在[ **\_KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)中的[**KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)成员的**PropertyId**成员中指定0（如需要）。

以下属性集属于编解码器 API：

[CODECAPI\_视频\_编码器](codecapi-video-encoder.md)

[CODECAPI\_音频\_编码器](codecapi-audio-encoder.md)

[CODECAPI\_SETALLDEFAULTS](codecapi-setalldefaults.md)

[CODECAPI\_ALLSETTINGS](codecapi-allsettings.md)

[CODECAPI\_SUPPORTSEVENTS](codecapi-supportsevents.md)

[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)

以下属性集属于编码器 API：

[ENCAPIPARAM\_比特率](encapiparam-bitrate.md)

[ENCAPIPARAM\_比特率\_模式](encapiparam-bitrate-mode.md)

[ENCAPIPARAM\_高峰\_比特率](encapiparam-peak-bitrate.md)

 

 





