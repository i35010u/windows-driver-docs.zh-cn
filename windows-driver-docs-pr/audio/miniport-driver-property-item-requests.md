---
title: 微型端口驱动程序属性项请求
description: 微型端口驱动程序属性项请求
ms.assetid: 37baad27-539b-46ab-b300-175bc0c2b992
keywords:
- 属性项请求 WDK DirectMusic
- 微型端口驱动程序 WDK 音频，属性项请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adc7d851ce3e5bd3befe1ad008b4b13e94e4fdd1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211371"
---
# <a name="miniport-driver-property-item-requests"></a>微型端口驱动程序属性项请求


## <span id="miniport_driver_property_item_requests"></span><span id="MINIPORT_DRIVER_PROPERTY_ITEM_REQUESTS"></span>


本部分简要介绍了 DirectMusic 属性项请求。 可以在 [内核流](../stream/kernel-streaming.md)中找到此和其他内核流式处理概念的完整概述。

DirectMusic 微型端口驱动程序必须处理 [音频驱动程序属性集](./audio-drivers-property-sets.md)。 属性请求分为两部分。 第一部分是 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构定义的属性集。 第二个是包含特定于属性项的实例数据的数据缓冲区。

KSPROPERTY 结构包含以下内容：

-   指定集 (的预定义 GUID) 例如 [KSPROPSETID \_ 合成 \_ dl](./kspropsetid-synth-dls.md) 。

-   指定集合中的属性项的项 ID (例如 [**KSPROPERTY \_ 合成 \_ DLS \_ **](/previous-versions/ff537396(v=vs.85))) 。

-   指定所请求操作的标志。

KSPROPERTY 的 **flags** 成员可能只包含以下标志之一来指定微型端口驱动程序请求的操作：

<span id="KSPROPERTY_TYPE_GET"></span><span id="ksproperty_type_get"></span>KSPROPERTY \_ 类型 \_ GET  
检索给定属性项的值。

<span id="KSPROPERTY_TYPE_SET"></span><span id="ksproperty_type_set"></span>KSPROPERTY \_ 类型 \_ 集  
设置给定属性项的值。

<span id="KSPROPERTY_TYPE_BASICSUPPORT"></span><span id="ksproperty_type_basicsupport"></span>KSPROPERTY \_ 类型 \_ BASICSUPPORT  
确定属性集可用的支持类型。 * \* PvPropertyData*中返回的数据是一个 DWORD，其中包含一个或两个 KSPROPERTY \_ 类型 \_ GET 和 KSPROPERTY \_ 类型 \_ 集，指示可能的操作。

属性项请求的第二部分是实例数据，这是一个可用于向微型端口驱动程序传递数据的缓冲区。 使用此缓冲区的方式取决于请求是集还是 GET：

-   如果请求是 KSPROPERTY \_ 类型 \_ 集，则实例数据将发送到微型端口驱动程序，但不会返回给请求者。

-   如果请求是 KSPROPERTY \_ 类型 \_ GET，则在微型端口驱动程序中填充实例数据并将其返回给请求者。

属性项请求可定向到微型端口驱动程序拓扑中的特定节点。 微型端口驱动程序拓扑描述了驱动程序和基础硬件的布局。 拓扑中可以是可以发送属性项的节点，无论在请求时是否有 pin 实例可用。

必须创建 pin 实例才能播放 DirectMusic。 DirectMusic 数据将发送到 [**KSNODETYPE \_ DMSYNTH**](./ksnodetype-dmsynth.md)类型的节点。 下面是微型端口驱动程序连接的示例：

-   将流连接到合成：

    PCFILTER \_ 节点引脚 0 (out) - &gt; Node 0 引脚 1 (in) 

-   将合成连接到音频输出：

    节点0引脚 0 (out) - &gt; PCFILTER \_ 节点 pin 1 (在) 

支持的数据格式是指定 pin 可在其中接收数据的格式的数据范围。

DirectMusic 格式 (静态 \_ KSDATAFORMAT \_ 子类型 \_ DirectMusic) 必须在微型端口驱动程序的拓扑中定义，以便 DirectMusic 可以将其数据发送到微型端口驱动程序。 此格式由 DMU \_ EVENTHEADER 结构定义 (参阅 dmusbuff 中的 Microsoft Windows SDK 文档) 。 当微型端口驱动程序指定它支持此特定数据范围时，DirectMusic 可以通过端口本身) 的 pin 向用户 (公开此数据范围。

 

