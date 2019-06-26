---
title: 微型端口驱动程序属性项请求
description: 微型端口驱动程序属性项请求
ms.assetid: 37baad27-539b-46ab-b300-175bc0c2b992
keywords:
- 属性项请求 WDK DirectMusic
- 微型端口驱动程序 WDK 音频、 属性项请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c22fddd2c3dc5c885f5e6e2e563ef3cb7a6fa7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363220"
---
# <a name="miniport-driver-property-item-requests"></a>微型端口驱动程序属性项请求


## <span id="miniport_driver_property_item_requests"></span><span id="MINIPORT_DRIVER_PROPERTY_ITEM_REQUESTS"></span>


本部分将简要介绍 DirectMusic 属性项请求。 这和内核流式处理的其他概念的完整概述可在[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)。

DirectMusic 微型端口驱动程序必须处理[音频驱动程序的属性集](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)。 属性请求分为两个部分。 第一部分是由定义的属性集[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构。 第二个是包含特定于的属性项的实例数据的数据缓冲区。

KSPROPERTY 结构包含以下元素：

-   一个预定义的指定集的 GUID (如[KSPROPSETID\_合成\_Dls](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth-dls))。

-   指定在集内的属性项的项 ID (如[ **KSPROPERTY\_合成\_DLS\_下载**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85)))。

-   指定请求的操作的标志。

**标志**KSPROPERTY 成员可能包含以下标志来指定请求的微型端口驱动程序的操作之一：

<span id="KSPROPERTY_TYPE_GET"></span><span id="ksproperty_type_get"></span>KSPROPERTY\_TYPE\_GET  
若要检索给定的属性项的值。

<span id="KSPROPERTY_TYPE_SET"></span><span id="ksproperty_type_set"></span>KSPROPERTY\_TYPE\_SET  
将给定的属性项的值设置。

<span id="KSPROPERTY_TYPE_BASICSUPPORT"></span><span id="ksproperty_type_basicsupport"></span>KSPROPERTY\_类型\_BASICSUPPORT  
若要确定可用于属性集支持的类型。 中返回的数据 *\*pvPropertyData*是包含一个或两个 KSPROPERTY DWORD\_类型\_GET 和 KSPROPERTY\_类型\_设置，请表明哪些操作可使用。

属性项请求的第二部分是实例数据，这是可用于将数据传入或传出微型端口驱动程序传递的缓冲区。 如何使用此缓冲区是依赖于该请求是一组或 GET:

-   如果请求是 KSPROPERTY\_类型\_设置，实例数据发送到微型端口驱动程序但不是会返回给请求者。

-   如果请求是 KSPROPERTY\_类型\_获取，请填写微型端口驱动程序数据并将其返回给请求者的实例。

属性项请求可以定向到微型端口驱动程序拓扑中的特定节点。 微型端口驱动程序拓扑描述该驱动程序和基础硬件的布局。 拓扑中可以是的节点，以便进行发送属性项，是否有可用的 pin 实例在请求的时间。

必须为 DirectMusic 播放创建 pin 实例。 DirectMusic 数据发送到的节点类型[ **KSNODETYPE\_DMSYNTH**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dmsynth)。 下面是一个微型端口驱动程序连接的示例：

-   连接到合成器中的流：

    PCFILTER\_节点 Pin 0 （出站）-&gt; （中） 的节点 0 Pin 1

-   连接到音频输出合成器：

    节点 0 0 （扩展） 的 Pin&gt; PCFILTER\_节点 （中） 的 Pin 1

支持的数据格式是指定 pin 的格式的数据范围可以接收中的数据。

DirectMusic 格式 (静态\_KSDATAFORMAT\_子类型\_DIRECTMUSIC)，以便 DirectMusic 可以将其数据发送到微型端口驱动程序必须定义微型端口驱动程序的拓扑中。 此格式由 DMU\_EVENTHEADER 结构 （请参阅 Microsoft Windows SDK 文档） 中 dmusbuff.h。 当微型端口驱动程序指定时，它支持此特定的数据范围时，DirectMusic 可以公开 （通过端口本身上 pin) 向用户的数据范围。

 

 




