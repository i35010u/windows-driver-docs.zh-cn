---
title: 筛选器、引脚和节点属性
description: 筛选器、引脚和节点属性
ms.assetid: e0d52e97-459f-4095-9cf5-1474117ce66a
keywords:
- 音频属性 WDK，筛选器
- WDM 音频属性 WDK，筛选器
- 音频属性 WDK，pin
- WDM 音频属性 WDK，pin
- 音频属性 WDK，节点
- WDM 音频属性 WDK，节点
- 筛选器属性 WDK 音频
- 节点属性 WDK 音频
- KS WDK 音频筛选器、 属性请求
- 筛选 WDK 音频属性请求
- 筛选 WDK 音频，属性概述
- 节点 WDK 音频，属性概述
- pin WDK 音频，属性概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4776ad0dc678ee1b15d24d16f12fe48459f351b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333650"
---
# <a name="filter-pin-and-node-properties"></a>筛选器、引脚和节点属性


## <span id="filter_pin_and_node_properties"></span><span id="FILTER_PIN_AND_NODE_PROPERTIES"></span>


Microsoft Windows 驱动程序模型 (WDM) 音频驱动程序表示作为 KS 筛选器，将音频设备，则表示设备上的硬件缓冲区作为筛选器上的 pin。 当客户端将属性请求发送到其中一个筛选器或 pin 对象时，端口驱动程序将接收请求，并将请求路由到相应的属性处理程序中的端口驱动程序或微型端口驱动程序。

音频设备支持三种类型的属性：

-   **筛选器属性**

    筛选器属性是作为一个整体筛选器的属性，而不是特定的 pin 或筛选器中的节点的属性。 筛选器属性的请求指定筛选器句柄，但它们不指定节点 Id。

-   **Pin 属性**

    Pin 属性是特定 pin 实例的筛选器上的属性。 这些属性的请求指定 pin 句柄，但它们不指定节点 Id。

-   **节点属性**

    节点属性是筛选器中的拓扑节点的属性。 节点属性的请求指定的筛选器句柄或 pin 句柄，加上一个节点 id。

节点属性请求指定的筛选器还是固定句柄取决于该节点是唯一的筛选器。 有关详细信息，请参阅以下节点属性部分。

下图显示了以下三种类型的属性请求： pin 属性请求发送到一个 pin 实例中，节点属性请求发送到的节点 （上一个筛选器或 pin 实例），并发送到筛选器实例的筛选器属性请求。

![说明筛选器、 pin 和节点属性请求的关系图](images/propreqs.png)

通常情况下，端口驱动程序处理最多请求的筛选器和 pin 属性，而微型端口驱动程序处理请求的节点属性。

端口驱动程序提供了自己内置的处理程序使用的筛选器和 pin 属性[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)(请参阅[KSPROPSETID\_Sysaudio](https://msdn.microsoft.com/library/windows/hardware/ff537489)和[KSPROPSETID\_Sysaudio\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff537490)) 和[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)。 微型端口驱动程序不需要实现端口驱动程序处理的属性的处理程序。 典型的微型端口驱动程序筛选器和 pin 属性提供了几个，如果有，处理程序。 微型端口驱动程序提供节点属性表示依赖于硬件的功能的音频设备的处理的程序。 端口驱动程序提供的节点属性没有内置处理除[ **KSPROPERTY\_拓扑\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff565809)。

在端口驱动程序和微型端口驱动程序提供相同的属性的处理程序时, 端口驱动程序使用自己的处理程序，并忽略微型端口驱动程序的处理程序。

### <a name="span-idfilterdescriptorsspanspan-idfilterdescriptorsspanspan-idfilterdescriptorsspanfilter-descriptors"></a><span id="Filter_Descriptors"></span><span id="filter_descriptors"></span><span id="FILTER_DESCRIPTORS"></span>筛选器描述符

端口驱动程序通过调用获取指向微型端口驱动程序的属性处理程序的指针[ **IMiniport::GetDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff536765)方法。 此方法中，通过端口驱动程序会检索指向微型端口驱动程序的筛选器描述符，这是类型的结构的指针[ **PCFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537694)。 此结构指定筛选器、 pin 和节点属性的微型端口驱动程序的属性处理的程序：

-   PCFILTER\_描述符结构**AutomationTable**成员指向的筛选器的自动化表。 此表指定筛选器属性的微型端口驱动程序的属性处理程序。

-   PCFILTER\_描述符结构**Pin**成员包含球瓶的自动化表。 每个表指定了特定的固定类型的固定属性的属性处理程序。

-   PCFILTER\_描述符结构**节点**成员包含在筛选器内部的拓扑节点的自动化表。 每个表指定了特定节点类型的节点属性的属性处理程序。

### <a name="span-idfilterpropertiesspanspan-idfilterpropertiesspanspan-idfilterpropertiesspanfilter-properties"></a><span id="Filter_Properties"></span><span id="filter_properties"></span><span id="FILTER_PROPERTIES"></span>筛选器属性

端口驱动程序访问微型端口驱动程序的筛选器属性处理程序通过**AutomationTable** PCFILTER 成员\_描述符。 通常情况下，此自动化表包含几个处理程序，因为端口驱动程序提供自己的 SysAudio 和 WDMAud 用于查询和配置音频设备的所有筛选器属性的内置处理程序。

但是，微型端口驱动程序可以提供筛选器属性的处理程序如[ **KSPROPERTY\_常规\_COMPONENTID** ](https://msdn.microsoft.com/library/windows/hardware/ff565171)提供依赖于硬件的信息不供端口驱动程序。 两个示例音频驱动程序中 Microsoft Windows Driver Kit (WDK) 处理 KSPROPERTY\_常规\_COMPONENTID 属性。 有关详细信息，请参阅 Msvad 和 Sb16 示例中的微型端口驱动程序实现。

Portcls.sys 中的所有端口驱动程序都提供用于处理[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)并[KSPROPSETID\_拓扑](https://msdn.microsoft.com/library/windows/hardware/ff566598)属性集。 这些字符集中的所有属性都筛选器属性都是除[ **KSPROPERTY\_拓扑\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff565809)，这是节点属性 （即使用了筛选器句柄，而不是 pin句柄，若要指定请求的目标）。 端口驱动程序支持的以下子集 KSPROPSETID\_Pin 属性：

[**KSPROPERTY\_PIN\_CATEGORY**](https://msdn.microsoft.com/library/windows/hardware/ff565192)

[**KSPROPERTY\_PIN\_CINSTANCES**](https://msdn.microsoft.com/library/windows/hardware/ff565193)

[**KSPROPERTY\_PIN\_通信**](https://msdn.microsoft.com/library/windows/hardware/ff565194)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565195)

[**KSPROPERTY\_PIN\_CTYPES**](https://msdn.microsoft.com/library/windows/hardware/ff565196)

[**KSPROPERTY\_PIN\_DATAFLOW**](https://msdn.microsoft.com/library/windows/hardware/ff565197)

[**KSPROPERTY\_PIN\_DATAINTERSECTION**](https://msdn.microsoft.com/library/windows/hardware/ff565198)

[**KSPROPERTY\_PIN\_DATARANGES**](https://msdn.microsoft.com/library/windows/hardware/ff565199)

[**KSPROPERTY\_PIN\_GLOBALCINSTANCES**](https://msdn.microsoft.com/library/windows/hardware/ff565200)

[**KSPROPERTY\_PIN\_INTERFACES**](https://msdn.microsoft.com/library/windows/hardware/ff565201)

[**KSPROPERTY\_PIN\_媒体**](https://msdn.microsoft.com/library/windows/hardware/ff565202)

[**KSPROPERTY\_PIN\_NAME**](https://msdn.microsoft.com/library/windows/hardware/ff565203)

[**KSPROPERTY\_PIN\_NECESSARYINSTANCES**](https://msdn.microsoft.com/library/windows/hardware/ff565204)

[**KSPROPERTY\_PIN\_PHYSICALCONNECTION**](https://msdn.microsoft.com/library/windows/hardware/ff565205)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff565206)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](https://msdn.microsoft.com/library/windows/hardware/dn567589)

这些属性提供有关属于筛选器的 pin 工厂的信息。 通常情况下，客户端创建 pin 实例之前查询这些属性的筛选器。 端口驱动程序支持全部四个 KSPROPSETID\_拓扑属性，它们提供有关筛选器的内部拓扑的信息。

此外，Dmu 端口驱动程序提供的处理程序[ **KSPROPERTY\_合成\_MASTERCLOCK** ](https://msdn.microsoft.com/library/windows/hardware/ff537403)属性，它是 DirectMusic 筛选器的只读属性。 KSPROPERTY\_合成\_MASTERCLOCK 所在[KSPROPSETID\_SynthClock](https://msdn.microsoft.com/library/windows/hardware/ff537487)属性集。

### <a name="span-idpinpropertiesspanspan-idpinpropertiesspanspan-idpinpropertiesspanpin-properties"></a><span id="Pin_Properties"></span><span id="pin_properties"></span><span id="PIN_PROPERTIES"></span>Pin 属性

端口驱动程序访问微型端口驱动程序的固定属性处理程序通过**插针**PCFILTER 成员\_描述符。 此成员指向 pin 描述符的数组和每个描述符指向 （固定 ID，它是只需数组索引标识） 的 pin 类型的自动化表。

通常情况下，这些自动化表包含几个条目，因为端口驱动程序提供自己的 SysAudio 和 WDMAud 使用的所有 pin 属性的处理程序。 微型端口驱动程序具有提供的一个或多个端口驱动程序不处理的 pin 属性处理程序的选项，但只有知道有关这些属性的客户端可以将属性请求发送它们。

除了拓扑端口驱动程序，Portcls.sys 中的所有端口驱动程序都提供以下固定属性的内置处理程序：

[**KSPROPERTY\_连接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff565110)

[**KSPROPERTY\_连接\_DATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff565103)

[**KSPROPERTY\_连接\_ALLOCATORFRAMING**](https://msdn.microsoft.com/library/windows/hardware/ff565099)

[**KSPROPERTY\_STREAM\_ALLOCATOR**](https://msdn.microsoft.com/library/windows/hardware/ff565684)

[**KSPROPERTY\_STREAM\_MASTERCLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff565713)

[**KSPROPERTY\_音频\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff537297)

[**KSPROPERTY\_DRMAUDIOSTREAM\_CONTENTID**](https://msdn.microsoft.com/library/windows/hardware/ff537351)

此列表中的属性的某些需要从微型端口驱动程序依赖于硬件的信息。 当端口驱动程序接收 IRP 包含这些属性之一的请求时，它不会不将 IRP 传递给微型端口驱动程序。 相反，端口驱动程序处理请求本身，但其处理程序获取所需的微型端口驱动程序中调用的入口点的信息。 例如，端口驱动程序提供其自己的属性处理程序为 KSPROPERTY\_音频\_位置请求。 此处理程序只需调用的微型端口驱动程序流**GetPosition**方法 (例如， [ **IMiniportWavePciStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536727)) 来获取当前的位置。

### <a name="span-idnodepropertiesspanspan-idnodepropertiesspanspan-idnodepropertiesspannode-properties"></a><span id="Node_Properties"></span><span id="node_properties"></span><span id="NODE_PROPERTIES"></span>节点属性

端口驱动程序访问微型端口驱动程序的节点属性处理程序通过**节点**PCFILTER 成员\_描述符。 此成员指向的节点描述符的数组和每个描述符指向 （节点 ID，它是只需数组索引标识） 的节点类型的自动化表。 通常情况下，所有或大多数属于微型端口驱动程序的属性处理程序位于**节点**数组。 音频驱动程序表示作为拓扑节点硬件控件中的音频设备，并使用属性机制依赖于硬件的控制设置为客户端提供访问权限。

如前面所述，客户端将筛选器属性请求发送到筛选器的句柄，并对 pin 句柄的 pin 属性请求。 不同于筛选器或 pin 实例中，节点不是内核对象，但没有一个句柄。 客户端将节点属性请求发送到固定句柄或筛选器句柄，但该请求还指定了节点 ID，以指示该请求是针对节点属性而不是 pin 或筛选器属性。

用于确定是否应使用筛选器句柄的节点属性或将其固定句柄的一般规则如下：

-   如果筛选器包含特定的固定类型的多个实例，该类型的每个 pin 包含具有特定的节点 ID 的节点，每个 pin 实例包含节点的实例。 在这种情况下，节点属性请求必须指定固定句柄 （而不只是一个筛选器句柄） 来区分相同节点类型的多个实例。 固定句柄和节点 ID 的组合明确标识特定的节点实例作为请求的目标。

-   如果筛选器包含一个特定的节点的一个实例，节点属性请求指定的筛选器句柄。 筛选器的句柄和节点 ID 的组合是不足以明确标识该请求的目标的节点。

在实施之前的特定节点属性的处理程序，但是，驱动程序编写器应参考[音频驱动程序的属性集](https://msdn.microsoft.com/library/windows/hardware/ff536197)若要检查是否应将该属性的目标指定为筛选器句柄或 pin 处理。

端口中的驱动程序 Portcls.sys 当前不提供内置处理的节点属性，除了 KSPROPERTY\_拓扑\_名称。

### <a name="span-idoverspecifiedandunderspecifiedpropertyrequestsspanspan-idoverspecifiedandunderspecifiedpropertyrequestsspanspan-idoverspecifiedandunderspecifiedpropertyrequestsspanoverspecified-and-underspecified-property-requests"></a><span id="Overspecified_and_Underspecified_Property_Requests"></span><span id="overspecified_and_underspecified_property_requests"></span><span id="OVERSPECIFIED_AND_UNDERSPECIFIED_PROPERTY_REQUESTS"></span>Overspecified 和 Underspecified 属性请求

驱动程序应准备好处理来自客户端不遵循上述规则的属性的请求。 请求可以 overspecified 或 underspecified:

-   **Overspecified 的请求**

    如果属性请求需要仅筛选器句柄，但客户端将请求发送到固定句柄相反，被 overspecified 请求的目标。 但是，驱动程序通常将请求视为有效，则为即，就好像它已被发送到包含固定的筛选器将该请求。

-   **Underspecified 的请求**

    如果属性请求要求提供 pin 的句柄，但客户端将请求发送到筛选器句柄相反，被 underspecified 请求的目标。 例如，如果筛选器包含多个 pin 实例具有相同的节点类型，并且客户端将该节点类型的属性的请求发送到筛选器句柄而不是 pin 句柄，驱动程序存在无法确定哪个节点实例应接收请求。 在这种情况下，行为取决于驱动程序。 而不是自动失败 underspecified 的所有请求，某些驱动程序视为 underspecified 的组属性请求有效。 在这种情况下的解释取决于该请求指定的节点 id。 设置的默认值 当 pin 工厂创建的新节点实例时，属于新节点的属性初始化为默认值。 更改默认值的请求在请求之前创建的节点实例无效。 此外，驱动程序统一失败 underspecified 的 get 属性请求因为处理程序无法确定哪个节点实例的属性的查询。

### <a name="span-idexceptionstotherulesspanspan-idexceptionstotherulesspanspan-idexceptionstotherulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>规则的例外情况

出于历史原因，一些音频属性具有的违反这些常规规则行为异常。 下面是一些示例：

-   如中所述[应用扬声器配置设置](applying-speaker-configuration-settings.md)，客户端可以通过设置更改音频设备的扬声器配置[ **KSPROPERTY\_音频\_通道\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537250)三维节点的属性 ([**KSNODETYPE\_3D\_效果**](https://msdn.microsoft.com/library/windows/hardware/ff537148))。 扬声器配置设置是全局的因为更改是通过扬声器播放设备组合的一部分的所有流的扬声器配置。 根据一般的规则，会影响整个筛选器的节点属性请求应指定筛选器句柄 （加上一个节点 ID）。 但是，这一特定属性需要 pin 句柄而不是筛选器句柄。 固定句柄指定包含该请求的目标的三维节点的 pin 实例。

-   [**KSPROPERTY\_合成\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff537409)并[ **KSPROPERTY\_合成器\_MASTERCLOCK** ](https://msdn.microsoft.com/library/windows/hardware/ff537403)是属性合成器节点 ([**KSNODETYPE\_合成器**](https://msdn.microsoft.com/library/windows/hardware/ff537203))。 尽管两者都是节点属性，这些属性的请求不包含节点 Id。 (请注意，该请求的属性描述符是类型的结构[ **KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)，而不[ **KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)。)此行为违反了一般的规则节点属性需要一个节点 id。 尽管这种差异，支持这两个属性的微型端口驱动程序应提供的属性处理程序通过**节点**PCFILTER 成员\_描述符 (而不是**Pin**成员）。

 

 




