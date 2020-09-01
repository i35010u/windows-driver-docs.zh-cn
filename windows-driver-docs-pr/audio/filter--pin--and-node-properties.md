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
- KS 筛选 WDK 音频，属性请求
- 筛选 WDK 音频，属性请求
- 筛选 WDK 音频，属性概述
- 节点 WDK 音频，属性概述
- 锁定 WDK 音频，属性概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c28b639a75a5c53d4165aedc0e96c63226482b59
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209237"
---
# <a name="filter-pin-and-node-properties"></a>筛选器、引脚和节点属性


## <span id="filter_pin_and_node_properties"></span><span id="FILTER_PIN_AND_NODE_PROPERTIES"></span>


Microsoft Windows 驱动模型 (WDM) 音频驱动程序将音频设备表示为 KS 筛选器，它们表示设备上的硬件缓冲区作为筛选器上的 pin。 当客户端向其中某个筛选器或固定对象发送属性请求时，端口驱动程序将接收请求，并将请求路由到端口驱动程序或微型端口驱动程序中的相应属性处理程序。

音频设备支持三种属性：

-   **筛选器属性**

    筛选器属性是筛选器中整个筛选器的属性，而不是特定的 pin 或节点的属性。 筛选器属性的请求指定筛选器句柄，但不指定节点 Id。

-   **固定属性**

    Pin 属性是筛选器上的特定 pin 实例的属性。 这些属性的请求指定了 pin 句柄，但不指定节点 Id。

-   **节点属性**

    节点属性是筛选器中的拓扑节点的属性。 节点属性的请求指定筛选器句柄或固定句柄以及节点 ID。

节点属性请求是指定筛选器还是指定固定句柄取决于该节点对于筛选器是否唯一。 有关详细信息，请参阅以下节点属性部分。

下图显示了这三种属性请求：发送到 pin 实例的 pin-属性请求、发送到 (筛选器或 pin 实例上的节点的节点属性请求) ，以及发送到筛选器实例的筛选器属性请求。

![说明筛选器、固定和节点属性请求的关系图](images/propreqs.png)

通常，端口驱动程序处理筛选器和 pin 属性的大多数请求，微型端口驱动程序处理节点属性的请求。

端口驱动程序为 [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver) 使用的筛选器和固定属性提供自己的内置处理程序 (参阅 [KSPROPSETID \_ SysAudio](./kspropsetid-sysaudio.md) 和 [KSPROPSETID \_ SysAudio \_ pin](./kspropsetid-sysaudio-pin.md)) 和 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)。 微型端口驱动程序无需实现端口驱动程序处理的属性的处理程序。 典型的微型端口驱动程序提供了少量的、适用于筛选器和固定属性的处理程序。 微型端口驱动程序为表示音频设备的硬件相关功能的节点属性提供处理程序。 端口驱动程序不提供节点属性的内置处理， [**KSPROPERTY \_ 拓扑 \_ 名称**](../stream/ksproperty-topology-name.md)除外。

当端口驱动程序和微型端口驱动程序为同一属性提供处理程序时，端口驱动程序将使用其自己的处理程序，并忽略微型端口驱动程序的处理程序。

### <a name="span-idfilter_descriptorsspanspan-idfilter_descriptorsspanspan-idfilter_descriptorsspanfilter-descriptors"></a><span id="Filter_Descriptors"></span><span id="filter_descriptors"></span><span id="FILTER_DESCRIPTORS"></span>筛选器描述符

端口驱动程序通过调用 [**IMiniport：： GetDescription**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription) 方法获取指向微型端口驱动程序的属性处理程序的指针。 通过此方法，端口驱动程序检索指向微型端口驱动程序的筛选器描述符的指针，这是 [**PCFILTER \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)类型的结构。 此结构为筛选器、固定和节点属性指定微型端口驱动程序的属性处理程序：

-   PCFILTER \_ 描述符结构的 **AutomationTable** 成员指向筛选器的自动化表。 此表指定了用于筛选器属性的微型端口驱动程序的属性处理程序。

-   PCFILTER \_ 描述符结构的 **pin** 成员包含 pin 的自动化表。 每个表都指定特定 pin 类型的 pin 属性的属性处理程序。

-   PCFILTER \_ 描述符结构的 **节点** 成员包含筛选器内的拓扑节点的自动化表。 每个表为特定节点类型的节点属性指定属性处理程序。

### <a name="span-idfilter_propertiesspanspan-idfilter_propertiesspanspan-idfilter_propertiesspanfilter-properties"></a><span id="Filter_Properties"></span><span id="filter_properties"></span><span id="FILTER_PROPERTIES"></span>筛选器属性

端口驱动程序通过 PCFILTER 描述符的 **AutomationTable** 成员访问微型端口驱动程序的筛选器属性处理程序 \_ 。 通常，此自动化表包含很少的处理程序，因为端口驱动程序为所有筛选器属性（SysAudio 和 WDMAud 用于查询和配置音频设备）提供自己的内置处理程序。

但是，微型端口驱动程序可以提供筛选器属性（如 [**KSPROPERTY \_ 常规 \_ 组件 id**](../stream/ksproperty-general-componentid.md) ）的处理程序，该组件提供了与硬件相关的信息不可用于端口驱动程序。 Microsoft Windows 驱动程序 (工具包中的两个示例音频驱动程序) 处理 KSPROPERTY \_ 常规 \_ 组件程序属性。 有关详细信息，请参阅 Msvad 和 Sb16 示例中的微型端口驱动程序实现。

Portcls.sys 中的所有端口驱动程序都提供对 [KSPROPSETID \_ Pin](../stream/kspropsetid-pin.md) 和 [KSPROPSETID \_ 拓扑](../stream/kspropsetid-topology.md) 属性集的处理。 这些集合中的所有属性都是筛选器属性，但 [**KSPROPERTY \_ 拓扑 \_ 名称**](../stream/ksproperty-topology-name.md)除外，它是一个节点属性 (，它使用筛选器句柄而不是 pin 句柄来指定请求) 的目标。 端口驱动程序支持以下 KSPROPSETID \_ Pin 属性子集：

[**KSPROPERTY \_ PIN \_ 类别**](../stream/ksproperty-pin-category.md)

[**KSPROPERTY \_ PIN \_ CINSTANCES**](../stream/ksproperty-pin-cinstances.md)

[**KSPROPERTY \_ PIN \_ 通信**](../stream/ksproperty-pin-communication.md)

[**KSPROPERTY \_ PIN \_ CONSTRAINEDDATARANGES**](../stream/ksproperty-pin-constraineddataranges.md)

[**KSPROPERTY \_ PIN \_ CTYPES**](../stream/ksproperty-pin-ctypes.md)

[**KSPROPERTY \_ PIN \_ 数据流**](../stream/ksproperty-pin-dataflow.md)

[**KSPROPERTY \_ PIN \_ DATAINTERSECTION**](../stream/ksproperty-pin-dataintersection.md)

[**KSPROPERTY \_ PIN \_ DATARANGES**](../stream/ksproperty-pin-dataranges.md)

[**KSPROPERTY \_ PIN \_ GLOBALCINSTANCES**](../stream/ksproperty-pin-globalcinstances.md)

[**KSPROPERTY \_ PIN \_ 接口**](../stream/ksproperty-pin-interfaces.md)

[**KSPROPERTY \_ PIN \_ 媒体**](../stream/ksproperty-pin-mediums.md)

[**KSPROPERTY \_ PIN \_ 名称**](../stream/ksproperty-pin-name.md)

[**KSPROPERTY \_ PIN \_ NECESSARYINSTANCES**](../stream/ksproperty-pin-necessaryinstances.md)

[**KSPROPERTY \_ PIN \_ PHYSICALCONNECTION**](../stream/ksproperty-pin-physicalconnection.md)

[**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT**](../stream/ksproperty-pin-proposedataformat.md)

[**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2**](../stream/ksproperty-pin-proposedataformat2.md)

这些属性提供有关属于筛选器的 pin 工厂的信息。 通常，客户端会在创建 pin 实例之前查询这些属性的筛选器。 端口驱动程序支持全部四个 KSPROPSETID \_ 拓扑属性，这些属性提供有关筛选器内部拓扑的信息。

此外，Dmu 端口驱动程序还为 [**KSPROPERTY \_ 合成 \_ MASTERCLOCK**](/previous-versions/ff537403(v=vs.85)) 属性提供了一个处理程序，它是 DirectMusic 筛选器的一个只读属性。 KSPROPERTY \_ 合成 \_ MASTERCLOCK 是 [KSPROPSETID \_ SynthClock](./kspropsetid-synthclock.md) 属性集的成员。

### <a name="span-idpin_propertiesspanspan-idpin_propertiesspanspan-idpin_propertiesspanpin-properties"></a><span id="Pin_Properties"></span><span id="pin_properties"></span><span id="PIN_PROPERTIES"></span>固定属性

端口驱动程序通过 PCFILTER 描述符的 **pin** 成员访问微型端口驱动程序的 pin 属性处理程序 \_ 。 此成员指向 pin 描述符的数组，每个描述符指向 (的 pin 类型的自动化表，该 ID 只是数组索引) 。

通常，这些自动化表包含几个条目，因为端口驱动程序为 SysAudio 和 WDMAud 使用的所有 pin 属性提供自己的处理程序。 微型端口驱动程序可以选择为端口驱动程序未处理的一个或多个 pin 属性提供处理程序，但只有知道这些属性的客户端可以发送其属性请求。

除了拓扑端口驱动程序，Portcls.sys 中的所有端口驱动程序都提供以下 pin 属性的内置处理程序：

[**KSPROPERTY \_ 连接 \_ 状态**](../stream/ksproperty-connection-state.md)

[**KSPROPERTY \_ 连接 \_ DATAFORMAT**](../stream/ksproperty-connection-dataformat.md)

[**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING**](../stream/ksproperty-connection-allocatorframing.md)

[**KSPROPERTY \_ 流 \_ 分配器**](../stream/ksproperty-stream-allocator.md)

[**KSPROPERTY \_ 流 \_ MASTERCLOCK**](../stream/ksproperty-stream-masterclock.md)

[**KSPROPERTY \_ 音频 \_ 位置**](./ksproperty-audio-position.md)

[**KSPROPERTY \_ DRMAUDIOSTREAM \_ ID 为**](/previous-versions/ff537351(v=vs.85))

此列表中的某些属性需要微型端口驱动程序中的硬件相关信息。 当端口驱动程序收到一个 IRP，其中包含其中一个属性的请求时，它不会将 IRP 传递到微型端口驱动程序。 相反，端口驱动程序会处理请求本身，但其处理程序会通过调用微型端口驱动程序中的入口点来获取所需的信息。 例如，端口驱动程序为 KSPROPERTY \_ 音频位置请求提供自己的属性处理程序 \_ 。 此处理程序只需调用微型端口驱动程序流的 **GetPosition** 方法 (例如， [**IMiniportWavePciStream：： GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)) 获取当前位置。

### <a name="span-idnode_propertiesspanspan-idnode_propertiesspanspan-idnode_propertiesspannode-properties"></a><span id="Node_Properties"></span><span id="node_properties"></span><span id="NODE_PROPERTIES"></span>节点属性

端口驱动程序通过 PCFILTER 描述符的 **节点** 成员访问微型端口驱动程序的节点属性处理程序 \_ 。 此成员指向节点说明符的数组，每个描述符指向节点类型的自动化表 (由节点 ID 标识，这只是数组索引) 。 通常，属于某个小型端口驱动程序的所有或大部分属性处理程序都位于 **节点** 数组中。 音频驱动程序表示音频设备中作为拓扑节点的硬件控件，并使用属性机制为客户端提供对硬件相关的控制设置的访问权限。

如前文所述，客户端将筛选器属性请求发送到筛选器句柄，并向 pin 句柄发送 pin 属性请求。 与筛选器或固定实例不同，节点不是内核对象，也没有句柄。 客户端向固定句柄或筛选器句柄发送节点-属性请求，但该请求还指定一个节点 ID，以指示该请求针对的是节点属性，而不是 pin 或筛选器属性。

下面是用于确定节点属性是应使用筛选器句柄还是固定句柄的一般规则：

-   如果筛选器包含特定 pin 类型的多个实例，并且该类型的每个 pin 都包含一个具有特定节点 ID 的节点，则每个 pin 实例都包含一个节点实例。 在这种情况下，节点属性请求必须指定一个 pin 句柄 (而不只是一个筛选器句柄) 来区分同一节点类型的多个实例。 固定句柄和节点 ID 的组合清楚地标识特定节点实例作为请求的目标。

-   如果筛选器只包含特定节点的一个实例，则节点属性请求将指定筛选器句柄。 筛选器句柄和节点 ID 的组合足以明确标识作为请求目标的节点。

但是，在为特定节点属性实现处理程序之前，驱动程序编写器应引用 [音频驱动程序属性集](./audio-drivers-property-sets.md) ，以检查是否应将属性的目标指定为筛选器句柄或固定句柄。

Portcls.sys 中的端口驱动程序当前不提供节点属性的内置处理，KSPROPERTY \_ 拓扑 \_ 名称除外。

### <a name="span-idoverspecified_and_underspecified_property_requestsspanspan-idoverspecified_and_underspecified_property_requestsspanspan-idoverspecified_and_underspecified_property_requestsspanoverspecified-and-underspecified-property-requests"></a><span id="Overspecified_and_Underspecified_Property_Requests"></span><span id="overspecified_and_underspecified_property_requests"></span><span id="OVERSPECIFIED_AND_UNDERSPECIFIED_PROPERTY_REQUESTS"></span>Overspecified 和 Underspecified 属性请求

应准备好驱动程序来处理来自不遵循上述规则的客户端的属性请求。 请求可以是 overspecified 或 underspecified：

-   **Overspecified 请求**

    如果属性请求只需要筛选器句柄，但客户端将请求发送到 pin 句柄，则请求的目标为 overspecified。 但是，驱动程序通常会将该请求视为有效的;也就是说，它们将请求视为发送到包含 pin 的筛选器。

-   **Underspecified 请求**

    如果属性请求需要 pin 句柄，但客户端将请求发送到筛选器句柄，则请求的目标为 underspecified。 例如，如果筛选器包含多个具有相同节点类型的 pin 实例，并且客户端将该节点类型的属性请求发送到筛选器句柄而不是 pin 句柄，则驱动程序无法确定哪个节点实例应接收请求。 在这种情况下，行为取决于驱动程序。 某些驱动程序将 underspecified 的 underspecified 请求视为有效，而不是自动失败所有的请求。 在这种情况下，解释是指请求为指定的节点 ID 设置默认值。 当 pin 工厂创建新的节点实例时，属于新节点的属性将初始化为默认值。 更改默认值的请求不会影响在请求之前创建的节点实例。 此外，驱动程序会统一地 underspecified get 属性请求，因为处理程序无法确定要查询属性的节点实例。

### <a name="span-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>规则的例外

由于历史原因，少数音频属性具有违反这些常规规则的行为兼容。 下面是一些示例：

-   如 [应用扬声器配置设置](applying-speaker-configuration-settings.md)中所述，客户端可以通过设置3-d 节点的 [**KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG**](./ksproperty-audio-channel-config.md) 属性来更改音频设备的扬声器配置，)  ([**KSNODETYPE \_ 三维 \_ 效果**](./ksnodetype-3d-effects.md) 。 扬声器配置设置是全局性的，因为它会更改所有流的扬声器配置，这些流是设备通过扬声器播放的组合的一部分。 根据常规规则，影响筛选器作为整体的节点属性请求应指定筛选器句柄 (加上节点 ID) 。 但是，此特定属性需要 pin 句柄而不是筛选器句柄。 Pin 控点指定包含作为请求目标的3-d 节点的 pin 实例。

-   [**KSPROPERTY \_合成 \_ VOLUME**](/previous-versions/ff537409(v=vs.85)) 和 [**KSPROPERTY \_ 合成 \_ MASTERCLOCK**](/previous-versions/ff537403(v=vs.85)) 是合成节点 ([**KSNODETYPE \_ 合成**](./ksnodetype-synthesizer.md) 器) 的属性。 尽管两者都是节点属性，但对这些属性的请求不包括节点 Id。  (注意，请求的属性描述符是 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))类型的结构，而不是 [**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)。 ) 此行为违反了 NODE 属性需要节点 ID 的一般规则。 尽管存在这种差异，但是，支持任一 **属性的微型** 端口驱动程序应通过 PCFILTER \_ 描述符 (而不是 **pin** 成员) 来提供属性处理程序。

 

