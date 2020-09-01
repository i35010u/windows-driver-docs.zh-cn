---
title: 音频属性的基本支持查询
description: 音频属性的基本支持查询
ms.assetid: d08b6f86-e4fd-4b2c-bfaa-191bcbac3ff8
keywords:
- 音频属性 WDK，基本支持查询
- WDM 音频属性 WDK，基本支持查询
- 基本-支持查询 WDK 音频
- 设置-属性 WDK 音频
- 有效范围 WDK 音频
- 范围值 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46c7e7443e3ff3e27ef107f0f288754f4218495d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208239"
---
# <a name="basic-support-queries-for-audio-properties"></a>音频属性的基本支持查询


## <span id="basic_support_queries_for_audio_properties"></span><span id="BASIC_SUPPORT_QUERIES_FOR_AUDIO_PROPERTIES"></span>


为筛选器、pin 或节点指定设置属性请求的数据时，客户端通常需要知道为属性指定的一个或多个值的有效数据范围。 范围可能因设备而异，甚至可能是从节点到相同设备中的节点。

某些属性定义为允许设置属性请求指定超出范围的值，但微型端口驱动程序会以静默方式将这些值固定到受支持的范围 (例如，请参阅 [**KSPROPERTY \_ AUDIO \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md)) 。 对于同一个属性，后续的 get 请求将检索该驱动程序的值或值的实际设置，这些设置可能是客户端在设置请求中指定的值的限制版本。

但是，客户端可能需要知道属性值的范围，而不是只依靠微型端口驱动程序来自动固定超出范围的值。 例如，为音频设备提供音量控制滑块的窗口化应用程序可能需要知道设备的卷范围才能将该范围映射到滑块的全长长度。

特定属性的驱动程序例程应能够提供范围信息以响应基本支持属性请求 (KSPROPERTY \_ 类型 \_ BASICSUPPORT) 。 向驱动程序发送 "基本支持" 属性请求时，客户端会提供一个值缓冲区，属性处理程序会将基本支持信息写入其中，其中包含一个 [**KSPROPERTY 的 \_ 描述**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description) 结构，该结构可能后跟属性特定数据。 此数据通常包含一个或多个参数范围的规范，具体取决于属性。

通常情况下，客户端不会提前知道此值缓冲区应为多大，并且必须向属性处理程序发送一两个初步请求，才能确定值大小。 这些初步请求的格式已定义良好。 当处理基本支持请求时，客户端应遵循以下约定：

-   如果请求将值大小指定为 **sizeof** (ULONG) 则属性处理程序应将 KSPROPERTY 说明结构的 **AccessFlags** 成员的值写入 \_ ULONG 大小的值缓冲区。 \_ \_ 如果该处理程序为基本支持属性请求提供进一步支持，则该处理程序将设置 KSPROPERTY 类型 BASICSUPPORT 标志位。

-   如果请求将值大小指定为 **sizeof** (KSPROPERTY \_ DESCRIPTION) ，则处理程序应将 KSPROPERTY \_ 说明结构写入数据缓冲区。 处理程序将结构的 " **DescriptionSize** " 字段设置为等于该结构的大小，以及该处理程序可用于加载到结构后面的数据缓冲区中的所有其他属性特定信息的大小。 这是需要为包含属性的基本支持信息的客户端分配的值缓冲区大小。

-   如果请求指定的值大小足以同时包含 KSPROPERTY \_ 说明结构和特定于属性的信息，则处理程序应将 KSPROPERTY \_ 说明结构写入缓冲区的开头，并且应将特定于属性的信息写入到位于 KSPROPERTY 说明结构末尾的数据缓冲区部分 \_ 。 编写 KSPROPERTY \_ 说明结构时，处理程序应将 **DescriptionSize** 字段设置为该结构的大小，并将该结构后面的特定于属性的信息的大小设置为。

如果请求指定的值大小与这三个事例之一不匹配，则属性处理程序将拒绝该请求并返回状态代码状态 \_ 缓冲区 \_ 太 \_ 小。

处理程序写入到值缓冲区中的属性特定信息可能包含属性值的数据范围。 KSPROPERTY MEMBERSHEADER 的 **MembersSize** 成员 \_ 表明是否包含数据范围：

-   如果不需要范围， **MembersSize**为零。 例如，如果属性值的类型为 BOOL，就会出现这种情况。

-   **MembersSize**如果 KSPROPERTY \_ MEMBERSHEADER 结构后跟一个或多个属性值的范围说明符，则 MembersSize 为非零值。

对于类型为 BOOL 的属性值，不需要范围说明符，因为范围隐式限制为值 **TRUE** 和 **FALSE**。 但是，需要范围描述符来指定具有整数类型的属性值的范围。

例如，对卷节点上的 [**KSPROPERTY \_ AUDIO \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md) 属性的基本支持请求 ([**KSNODETYPE \_ 卷**](./ksnodetype-volume.md)) 检索该节点的最小和最大卷设置。 在这种情况下，客户端需要分配一个足够大的值缓冲区来包含以下结构：

[**KSPROPERTY \_ 说明**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description)

[**KSPROPERTY \_ MEMBERSLIST**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_memberslist)

[**KSPROPERTY \_ 步进 \_ 长**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)

这三个结构按前面列表中显示的顺序打包到缓冲区中的相邻位置。 处理请求时，微型端口驱动程序将最小和最大音量级别写入**Bounds**到 KSPROPERTY \_ 单步执行长结构的边界成员中 \_ 。

有关包含范围说明符数组的基本支持请求的示例，请参阅 [公开多通道节点](exposing-multichannel-nodes.md)中的图。 有关基本支持属性请求的详细信息，请参阅 [KS 属性](../stream/ks-properties.md)。 有关代码示例，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中的 [示例音频驱动程序](sample-audio-drivers.md) 中的属性处理程序实现。

 

