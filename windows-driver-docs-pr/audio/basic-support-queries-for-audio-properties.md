---
title: 基本支持查询的音频属性
description: 基本支持查询的音频属性
ms.assetid: d08b6f86-e4fd-4b2c-bfaa-191bcbac3ff8
keywords:
- 音频属性 WDK，basic 支持的查询
- WDM 音频属性 WDK，basic 支持的查询
- basic 支持查询 WDK 音频
- 设置属性 WDK 音频
- 有效范围 WDK 音频
- 范围值 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be69fde2d31986b3459dc859b123674dc3f215bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545125"
---
# <a name="basic-support-queries-for-audio-properties"></a>基本支持查询的音频属性


## <span id="basic_support_queries_for_audio_properties"></span><span id="BASIC_SUPPORT_QUERIES_FOR_AUDIO_PROPERTIES"></span>


指定对筛选器、 pin 或节点的设置属性请求数据，客户端经常需要知道，它指定属性的值的有效的数据范围。 范围可以在同一设备内改变设备的和可能甚至从节点到节点。

某些属性定义为允许设置属性指定值超出范围的请求，但微型端口驱动程序以无提示方式将这些值与支持的范围 (有关示例，请参阅[ **KSPROPERTY\_音频\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309))。 相同属性的后续的 get 请求检索驱动程序的实际设置的值或值，这可能是限制的版本的客户端设置在请求中指定的值。

但是，客户端可能需要知道而不是简单地依靠微型端口驱动程序会自动将超出范围值的属性值的范围。 例如，窗口中应用程序，其中的一个音量控制滑块，用于将音频设备可能需要知道设备的卷范围，才能将该范围映射到滑块的完整长度。

对于特定属性的驱动程序的处理程序例程应能够提供基本支持属性请求的响应中的范围信息 (KSPROPERTY\_类型\_BASICSUPPORT)。 当 basic 支持属性请求发送到驱动程序，客户端提供的属性处理程序在其中写入 basic 支持信息，其中包括的值缓冲区[ **KSPROPERTY\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff565132)可能跟属性特定于数据的结构。 此数据通常包含一个或多个参数范围，具体取决于属性的规范。

一般情况下，客户端不知道此值缓冲区应事先了解大型并必须将一个或两个预备请求发送到的属性处理程序，以确定值的大小。 这些预备请求的格式是定义完善的。 客户端预期驱动程序，以处理 basic 支持请求时遵循以下约定：

-   如果该请求指定了具有值的大小**sizeof**(ULONG) 然后属性处理程序应写入的值**AccessFlags** KSPROPERTY 成员\_描述结构ULONG 大小的值的缓冲区。 该处理程序设置 KSPROPERTY\_类型\_BASICSUPPORT 标志位，如果提供了进一步的支持的基本支持属性请求。

-   如果该请求指定了具有值的大小**sizeof**(KSPROPERTY\_说明)，该处理程序应编写 KSPROPERTY\_描述结构的数据缓冲区。 处理程序集**DescriptionSize**字段的结构等于该结构的大小加上其大小、 特定属性的附加信息的所有处理程序具有可用于加载到数据缓冲区以下结构。 这是客户端需要分配以包含该属性的基本支持信息的值缓冲区的大小。

-   如果该请求指定了值大小足以包含这两个 KSPROPERTY\_描述结构和特定于属性的信息，该处理程序应编写 KSPROPERTY\_描述结构的开头缓冲区，和它应写入特定于属性的信息的数据缓冲区的 KSPROPERTY 结束之后的部分\_描述结构。 当编写 KSPROPERTY\_描述结构，该处理程序应设置**DescriptionSize**字段为该结构的大小加上遵循的结构的特定于属性的信息的大小。

如果该请求指定了这三种情况之一不匹配的值大小，将拒绝该请求的属性处理程序，并且返回状态代码状态\_缓冲区\_过\_小。

处理程序将写入到值缓冲区的特定于属性的信息可能包含属性值的数据范围。 **MembersSize** KSPROPERTY 成员\_MEMBERSHEADER 指示数据区域是否包含：

-   **MembersSize**为零，如果需要无范围。 这种，例如，如果属性值的类型 BOOL。

-   **MembersSize**为非零值如果 KSPROPERTY\_MEMBERSHEADER 结构后跟一个或多个属性值的范围说明符。

对于类型 BOOL 的属性值，因为范围被隐式限制为值需要没有范围描述符 **，则返回 TRUE**并**FALSE**。 但是，范围描述符所需的整数类型使用指定的属性值的范围。

例如，basic 支持请求[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)卷节点上的属性 ([**KSNODETYPE\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff537208)) 检索该节点的最小值和最大卷设置。 在这种情况下，客户端需要分配值的缓冲区足够大，以包含以下结构：

[**KSPROPERTY\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff565132)

[**KSPROPERTY\_MEMBERSLIST**](https://msdn.microsoft.com/library/windows/hardware/ff565190)

[**KSPROPERTY\_单步执行\_长**](https://msdn.microsoft.com/library/windows/hardware/ff565631)

三个结构都打包到上述列表中显示的顺序在缓冲区中的相邻位置。 微型端口驱动程序在处理请求时，写入到的最小值和最大卷级别**边界**KSPROPERTY 成员\_单步执行\_长时间结构。

与非数组范围说明符的 basic 支持请求的示例，请参阅中的图形[公开多通道节点](exposing-multichannel-nodes.md)。 有关基本支持属性请求的详细信息，请参阅[KS 属性](https://msdn.microsoft.com/library/windows/hardware/ff567671)。 有关代码示例，请参阅中的属性处理程序实现[示例音频驱动程序](sample-audio-drivers.md)Microsoft Windows Driver Kit (WDK) 中。

 

 




