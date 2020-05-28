---
title: WDI TLV 生成器/分析器 XML 语义
description: TLV 生成器/分析器 XML 文件是消息、容器（TLVs）和属性组（结构）的列表。 本主题介绍 XML 语法。
ms.assetid: AD268E68-B969-45D8-A2F2-4025E827D496
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f59ab54c77805620d7e7ad49812399faabe00f2
ms.sourcegitcommit: 97272cb572d24b1ac72669e51e5051089e1dd2c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "84053281"
---
# <a name="wdi-tlv-generatorparser-xml-semantics"></a>WDI TLV 生成器/分析器 XML 语义

TLV 生成器/分析器 XML 文件是消息、容器（TLVs）和属性组（结构）的列表。 本主题介绍 XML 语法。

- [`<message />`](#message-)
  - [特性](#attributes)
  - [内容](#content)
  - [示例](#example)
- [`<containerRef />`](#containerref-)
  - [特性](#containerref--attributes)
  - [内容](#container--contents)
  - [示例](#containerref--example)
- [`<containers />`](#containers-)
- [`<container />`](#container-)
  - [特性](#container--attributes)
  - [Contents](#container--contents)
  - [示例](#container--example)
- [`<groupRef />`](#groupref-)
  - [特性](#groupref--attributes)
  - [内容](#groupref--content)
  - [示例](#groupref--examples)
- [`<namedType />`](#namedtype-)
  - [特性](#namedtype--attributes)
  - [内容](#namedtype--content)
  - [示例](#namedtype--example)
- [`<aggregateContainer />`](#aggregatecontainer-)
  - [特性](#aggregatecontainer--attributes)
  - [内容](#aggregatecontainer--content)
  - [示例](#aggregatecontainer--example)
- [`<propertyGroups />`](#propertygroups-)
- [基元字段类型（ `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>` ）](#primitive-field-types-bool-uint8-uint16-uint32-int8-int16-int32)
  - [特性](#attributes-for-primitive-field-types)
  - [Contents](#contents-for-primitive-field-types)
- [`<propertyGroup />`](#propertygroup-)
  - [特性](#propertygroup--attributes)
  - [Contents](#propertygroup--contents)
  - [示例](#propertygroup--example)

## `<message />`

描述单个顶级 WDI 消息。 对于这些消息项，只有分析器/生成器函数。

### <a name="attributes"></a>属性

- `commandId`-必须在 dot11wdi 中定义的符号常数。
- `type`-要向代码公开的类型名称（在调用分析器/生成器函数时使用此类型）。
- `description`-命令的说明。
- `direction`-指示此消息是否描述了从 WDI 转到 IHV 微端口作为 M1 （称为 "ToIhv"）的一部分的 TLV 流，描述了 TLV 流，因为它从作为 M0、M3 或 M4 （称为 "FromIhv"）的 IHV 小型端口进入 WDI，或在两个方向（称为 "两个"）。 请参阅[WDI TLV parser interface 概述](wdi-tlv-parser-interface-overview.md)中的*消息方向*。

### <a name="content"></a>内容

容器引用（）的列表 `<containerRef />` 。 这些是组成消息的不同 TLVs。 它们是对在部分中定义的类型的引用 `<containers />` 。

### <a name="example"></a>示例

```XML
<message commandId="WDI_SET_P2P_LISTEN_STATE"
         type="WDI_SET_P2P_LISTEN_STATE_PARAMETERS"
         description="Parameters to set listen state."
         direction="ToIhv">
  <containerRef id="WDI_TLV_P2P_CHANNEL_NUMBER"
                name="ListenChannel"
                optional="true"
                type="WFDChannelContainer" />
  <containerRef id="WDI_TLV_P2P_LISTEN_STATE"
                name="ListenState"
                type="P2PListenStateContainer" />
</message>
```

## `<containerRef />`

对 `<container />` 节中定义的的引用 `<containers />` 。

### <a name="containerref--attributes"></a>`<containerRef />`属性

- `id`-必须在 wditypes 中定义的 TLV ID。
- `name`-父结构中的变量的名称。
- `optional`-指定它是否为可选字段。 默认值为 False。 生成的代码强制执行 "选择性"。
- `multiContainer`–指定生成的代码是否应期望多个相同类型的 TLVs。 默认值为 False。 如果为 false，则生成的代码强制仅存在其中一个。
- `type`-引用部分中特定元素的 "name" 属性 `<containers />` 。
- `versionAdded`-版本控制的一部分。 指示此 TLV 容器不应在与此特性中所指示的版本小于的对等方之间出现在字节流中。
- `versionRemoved`-版本控制的一部分。 指示此 TLV 容器不应在与此特性中所指示的版本大于或等于的对等方中出现在字节流中。

### <a name="containerref--content"></a>`<containerRef />`Content

无。

### <a name="containerref--example"></a>`<containerRef />` 示例

```XML
<containerRef id="WDI_TLV_P2P_CHANNEL_NUMBER"
              name="ListenChannel"
              optional="true"
              type="WFDChannelContainer"/>
```

## `<containers />`

描述 WDI 消息中使用的所有容器/TLVs。 可以将容器视为 TLV 存储桶。 有2种类型： `<container />` 和 `<aggregateContainer />` 。

## `<container />`

单个结构引用或命名类型的 TLV 容器。 它的大小是静态的，但也可以是 C 样式的数组，只要它是静态大小的。

### <a name="container--attributes"></a>`<container />`属性

- `name`-由 WDI 消息/其他容器引用的 ID。
- `description`-容器的用途的友好说明。
- `type`–要向代码公开的类型名称。
- `isCollection`-指定生成的代码是否应期望同一 TLV （C 样式数组）中有很多相同的大小元素。 默认值为 false （仅应有一个具有给定类型的元素）。
- `isZeroValid`-仅当 `isCollection` 为 true 时有效。 确定是否允许使用零元素数组。 当 TLV 流需要区分不存在的可选 TLV 与存在但长度为零（如 Ssid）的可选 TLV 时，这非常有用。 由于这种差异很少出现，因此默认值为 false。

### <a name="container--contents"></a>`<container />` 内容

`<groupRef />`或中的一个 `<namedType />` 。

### <a name="container--example"></a>`<container />` 示例

```XML
<container name="P2PListenStateContainer"
           description="Container for P2P Listen State setting."
           type="WDI_P2P_LISTEN_STATE_CONTAINER">
  <namedType name="ListenState"
             type="WDI_P2P_LISTEN_STATE"
             description="P2P Listen State."/>
</container>
```

## `<groupRef />`

对节中定义的属性组（结构）的引用 `<propertyGroups />` 。

### <a name="groupref--attributes"></a>`<groupRef />`属性

- `name`-父结构中结构的名称。
- `ref`-引用节中的命名结构 `<propertyGroups />` 。
- `description`–结构的用途的友好说明符。

### <a name="groupref--content"></a>`<groupRef />`Content

无。

### <a name="groupref--examples"></a>`<groupRef />` 示例

```XML
<container name="WFDChannelContainer"
           description="Container for a Wi-Fi Direct channel."
           type="WDI_P2P_CHANNEL_CONTAINER">
  <groupRef name="Channel"
            ref="WFDChannelStruct"
            description="Wi-Fi Direct Channel." />
</container>
```

## `<namedType />`

对由 wditypes、hpp 或 dot11wdi 公开的原始类型的引用。 使用默认序列化程序（memcpy），因此，由于存在填充问题，请使用自己的风险。

### <a name="namedtype--attributes"></a>`<namedType />`属性

- `name`-父结构中结构的名称。
- `type`-要在实际代码中使用的类型名称。
- `description`–结构的用途的友好说明。

### <a name="namedtype--content"></a>`<namedType />`Content

无。

### <a name="namedtype--example"></a>`<namedType />` 示例

```XML
<container name="P2PListenStateContainer"
           description="Container for P2P Listen State setting."
           type="WDI_P2P_LISTEN_STATE_CONTAINER">
  <namedType name="ListenState"
             type="WDI_P2P_LISTEN_STATE"
             description="P2P Listen State."/>
</container>
```

## `<aggregateContainer />`

许多不同容器的 TLV 容器。 这用于处理嵌套的 TLVs。

### <a name="-attributes"></a>`<aggregateContainer />`属性

- `name`-由 WDI 消息/其他容器引用的 ID。
- `description`-容器的用途的友好说明。
- `type`-要向代码公开的类型名称。

### <a name="-content"></a>`<aggregateContainer />`Content

列表 `<containerRef />` 。

### <a name="-example"></a>`<aggregateContainer />` 示例

```XML
<aggregateContainer
    name="P2PInvitationRequestInfoContainer"
    type="WDI_P2P_INVITATION_REQUEST_INFO_CONTAINER"
    description="Generic container for Invitation Request-related containers.">
  <containerRef
    id="WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS"
    type="P2PInvitationRequestParamsContainer"
    name="RequestParams" />
  <containerRef
    id="WDI_TLV_P2P_GROUP_BSSID"
    type="MacAddressContainer"
    name="GroupBSSID"
    optional="true" />
  <containerRef
    id="WDI_TLV_P2P_CHANNEL_NUMBER"
    type="WFDChannelContainer"
    name="OperatingChannel"
    optional="true" />
  <containerRef
    id="WDI_TLV_P2P_GROUP_ID"
    type="P2PGroupIDContainer"
    name="GroupID" />
</aggregateContainer>
```

## `<propertyGroups />`

描述所有容器中使用的所有结构。 结构可由使用 `<container />` 或由另一个 `<propertyGroup />` （嵌套结构）引用。 它们是独立于 TLVs 容器定义的，因此可以重复使用。 它们没有 TLV 标头。

这些定义是必需的，因为它们有助于解决与结构有关的填充问题，并提供代码生成器有关如何解释数据的说明。

>[!NOTE]
>这里的顺序很重要。 所有数据偏移均基于属性组说明隐含，数据按此处定义的顺序写入/分析。 这些结构必须在此处定义。

## <a name="primitive-field-types-bool-uint8-uint16-uint32-int8-int16-int32"></a>基元字段类型（ `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>` ）

这些是可用的基元类型，并由生成的代码适当地进行转换/封送。

### <a name="attributes-for-primitive-field-types"></a>基元字段类型的特性

- `name`-父结构中的字段名称。
- `description`–属性的含义的友好说明。
- `count`-给定属性有多少个。 默认值为1。 如果值大于1，则将此属性设置为代码中的静态大小的数组。

### <a name="contents-for-primitive-field-types"></a>基元字段类型的内容

无

## `<propertyGroup />`

单个结构。

### <a name="propertygroup--attributes"></a>`<propertyGroup />`属性

- `name`-由 WDI 消息/其他容器引用的 ID。
- `description`–属性组的用途的友好说明。
- `type`-要向代码公开的类型名称。

### <a name="propertygroup--contents"></a>`<propertyGroup />` 内容

有几种可能的属性类型（"结构" 字段）。

- `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`

- `<groupRef />`

- `<namedType />`

### <a name="propertygroup--example"></a>`<propertyGroup />` 示例

```XML
<propertyGroup name="P2PDiscoverModeStruct"
               type="WDI_P2P_DISCOVER_MODE"
               description="Structure definition for P2P Discover Mode Parameters">
  <namedType name="DiscoveryType"
             type="WDI_P2P_DISCOVER_TYPE"
             description="Type of discovery to be performed by the port."/>
  <bool name="ForcedDiscovery"
        description="A flag indicating that a complete device discovery is required. If this flag is not set, a partial discovery may be performed." />
  <namedType name="ScanType"
             type="WDI_P2P_SCAN_TYPE"
             description="Type of scan to be performed by port in scan phase." />
  <bool name="ScanRepeatCount"
        description="How many times the full scan procedure should be repeated. If set to 0, scan should be repeated until the task is aborted by the host."/>
</propertyGroup>
<propertyGroup name="P2PDeviceInfoParametersStruct"
               type="WDI_P2P_DEVICE_INFO_PARAMETERS"
               description="Structure definition for P2P Device Information Parameters.">
  <uint8 count="6"
         name="DeviceAddress"
         description="Peer's device address." />
  <uint16 name="ConfigurationMethods"
          description="Configuration Methods supported by this device." />
  <groupRef name="DeviceType"
            description="Primary Device Type."
            ref="WFDDeviceType" />
</propertyGroup>
```
