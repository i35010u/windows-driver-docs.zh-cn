---
title: 编码器属性集
description: 编码器属性集
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f200505706adde784756283e63cc3808731c5c82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837085"
---
# <a name="encoder-property-sets"></a>编码器属性集


## <span id="ddk_encoder_property_sets_ks"></span><span id="DDK_ENCODER_PROPERTY_SETS_KS"></span>


本部分介绍了编码器和编解码器 API 特定的属性集，这些属性集可用于在 Microsoft Windows 98/Me、Windows 2000 和 Windows XP 及更高版本中使用 WDM 内核流式处理服务的编码器微型驱动程序。

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

    这是向其发送属性请求的 KS 对象。 视频编码器属性的目标是筛选器或 pin。  (属性请求按其内核句柄指定目标对象。 ) 

-   **属性描述符类型**

    属性说明符指定属性和要对该属性执行的操作。 描述符始终以 [**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 结构开始。

-   **属性值类型**

    属性具有值，并且此值的类型取决于属性。 例如，一个只能处于两种状态的属性（打开或关闭）通常具有 BOOL 值。 可以假设从0x0 到0xFFFFFFFF 的整数值的属性可能具有 ULONG 值。 更复杂的属性可能具有作为数组或结构的值。

上面的属性说明符和属性值是在 [KS 属性、事件和方法](./ks-properties--events--and-methods.md)中讨论的实例规范和操作数据缓冲区的属性特定版本。

属性请求使用下列标志之一来指定要对属性执行的操作：

-   KSPROPERTY \_ 类型 \_ BASICSUPPORT

-   KSPROPERTY \_ 类型 \_ GET

-   KSPROPERTY \_ 类型 \_ 集

所有筛选器和 pin 对象均支持对其属性的基本支持操作。 它们是否支持 *get* 和 *Set* 操作取决于属性。 表示筛选器或固定对象的固有功能的属性可能只需要 *get* 操作。 尽管 *获取* 操作也可能对读取当前设置很有用，但表示可配置的设置的属性可能只需要 *设置* 操作。 若要详细了解如何使用带有视频编码器属性的 get、set 和 basic 支持操作，请参阅 [KS properties](./ks-properties.md)。

每个属性的说明中的表指示是否需要视频编码器微型驱动程序来支持读取或写入属性。 视频编码器微型驱动程序应返回对 \_ \_ 微型驱动程序不支持的属性的 get 或 set 请求所需的状态。

下面的每个属性集都包含一个属性，该属性必须由视频编码器微型驱动程序实现。 也就是说，每个属性都有其自己的集合，因此在 [**KSPROPERTY \_ 集**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)结构中的 [**KSPROPERTY \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)成员的 **PropertyId** 成员中指定0（根据需要）。

以下属性集属于编解码器 API：

[CODECAPI \_ 视频 \_ 编码器](codecapi-video-encoder.md)

[CODECAPI \_ 音频 \_ 编码器](codecapi-audio-encoder.md)

[CODECAPI \_ SETALLDEFAULTS](codecapi-setalldefaults.md)

[CODECAPI \_ ALLSETTINGS](codecapi-allsettings.md)

[CODECAPI \_ SUPPORTSEVENTS](codecapi-supportsevents.md)

[CODECAPI \_ CURRENTCHANGELIST](codecapi-currentchangelist.md)

以下属性集属于编码器 API：

[ENCAPIPARAM \_ 比特率](encapiparam-bitrate.md)

[ENCAPIPARAM \_ 比特率 \_ 模式](encapiparam-bitrate-mode.md)

[ENCAPIPARAM \_ 峰值 \_ 比特率](encapiparam-peak-bitrate.md)

 

