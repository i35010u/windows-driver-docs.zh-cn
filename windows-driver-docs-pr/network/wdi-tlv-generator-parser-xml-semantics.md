---
title: WDI TLV 分析器生成器/XML 语义
description: TLV 生成器/分析 XML 文件是一系列消息容器 (TLVs) 和属性进行分组 （结构）。 本主题介绍的 XML 语法。
ms.assetid: AD268E68-B969-45D8-A2F2-4025E827D496
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c5e5160eeec348b8e3c7392257cfe2d78e9e6d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385834"
---
# <a name="wdi-tlv-generatorparser-xml-semantics"></a>WDI TLV 分析器生成器/XML 语义


TLV 生成器/分析 XML 文件是一系列消息容器 (TLVs) 和属性进行分组 （结构）。 本主题介绍的 XML 语法。

-   [`<message />`](#-message---)
    -   [属性](#attributes)
    -   [Content](#content)
    -   [示例](#example)
-   [`<containerRef />`](#-containerref---)
    -   [属性](#attributes)
    -   [Content](#content)
    -   [示例](#example)
-   [`<containers />`](#-containers---)
-   [`<container />`](#-container---)
    -   [属性](#attributes)
    -   [内容](#contents)
    -   [示例](#example)
-   [`<groupRef />`](#-groupref---)
    -   [属性](#attributes)
    -   [Content](#content)
    -   [示例](#examples)
-   [`    <namedType />`](#--namedtype---)
    -   [属性](#attributes)
    -   [Content](#content)
    -   [示例](#example)
-   [`<aggregateContainer />`](#-aggregatecontainer---)
    -   [属性](#attributes)
    -   [Content](#content)
    -   [示例](#example)
-   [`<propertyGroups />`](#-propertygroups---)
-   [基元字段类型 (`<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`)](#primitive-field-types---bool----uint8----uint16----uint32----int8----int16----int32---)
    -   [属性](#attributes)
    -   [内容](#contents)
-   [`<propertyGroup />`](#-propertygroup---)
    -   [属性](#attributes)
    -   [内容](#contents)
    -   [示例](#example)

## `<message />`


描述单个顶级 WDI 消息。 有一些分析器/生成器函数仅为这些消息条目。

### <a name="attributes"></a>特性

-   `commandId` 必须在 dot11wdi.h 中定义的符号常量。
-   `type` 若要公开给 （到分析器/生成器的函数中调用时，您使用此类型） 的代码的类型名称。
-   `description` -该命令的说明。
-   `direction` – 指示是否此消息描述 TLV 流，因为它从 WDI 转到 M1 （称为"ToIhv"） 的一部分 IHV 微型端口，将相应地显示 IHV 微型端口到 WDI 为 M0、 M3 或 M4 （称为"FromIhv"），或进入 （名为两个方向，描述了 TLV 流 "Both")。 请参阅*消息方向*中[WDI TLV 分析器接口概述](wdi-tlv-parser-interface-overview.md)。

### <a name="content"></a>内容

容器引用的列表 (`<containerRef />`)。 这些是组成消息不同 TLVs。 它们是对类型中定义的引用`<containers />`部分。

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


引用`<container />`中定义`<containers />`部分。

### <a name="attributes"></a>特性

-   `id` -TLV 必须 wditypes.h 中定义的 ID。
-   `name` -父结构中的变量的名称。
-   `optional` -指定它是一个可选字段。 默认值为 false。 生成的代码强制实施"可选状态"。
-   `multiContainer` -指定在生成的代码应会相同类型的多个 TLVs。 默认值为 false。 如果为 false，强制执行生成的代码，只有一个已存在。
-   `type` -引用中的特定元素的"name"属性`<containers />`部分。
-   `versionAdded` -版本控制的一部分。 指示，此 TLV 容器不应出现在与对等方具有一个版本的字节流小于 1 指示此属性中。
-   `versionRemoved` -版本控制的一部分。 指示不应在向/从对等方具有的版本大于或等于此属性中指定的字节流中出现此 TLV 容器。

### <a name="content"></a>内容

无。

### <a name="example"></a>示例

```XML
<containerRef id="WDI_TLV_P2P_CHANNEL_NUMBER"
              name="ListenChannel"
              optional="true"
              type="WFDChannelContainer"/>
```

## `<containers />`


描述所有容器/TLVs WDI 消息中使用。 可以将容器视为 TLV 存储桶。 有两种类型：`<container />`和`<aggregateContainer />`。

## `<container />`


单个结构引用或命名的类型的 TLV 容器。 它以静态方式调整大小，但可能的 C 样式数组，只要以静态方式调整大小。

### <a name="attributes"></a>特性

-   `name` -ID 是所引用的 WDI 消息 / 其他容器。
-   `description` -容器是什么友好说明。
-   `type` – 若要向代码公开的类型名称。
-   `isCollection` -指定生成代码应期待许多相同 TLV （C 样式数组） 中的相同大小元素。 默认值为 false （仅需要给定类型的一个元素）。
-   `isZeroValid` -时仅有效`isCollection`为 true。 确定是否允许一个零个元素的数组。 当需要区分不存在与一个出现但长度为零 （如 Ssid) 可选 TLV TLV 流时，这很有用。 由于这一区别很少见，默认值为 false。

### <a name="contents"></a>目录

之一`<groupRef />`或`<namedType />`。

### <a name="example"></a>示例

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


对属性组 （结构） 中定义引用`<propertyGroups />`部分。

### <a name="attributes"></a>特性

-   `name` -父结构中的结构的名称。
-   `ref` -引用中的命名结构`<propertyGroups />`部分。
-   `description` – 结构使用友好描述符。

### <a name="content"></a>内容

无。

### <a name="examples"></a>示例

```XML
<container name="WFDChannelContainer"
           description="Container for a Wi-Fi Direct channel."
           type="WDI_P2P_CHANNEL_CONTAINER">
  <groupRef name="Channel"
            ref="WFDChannelStruct"
            description="Wi-Fi Direct Channel." />
</container>
```

## ` <namedType />`


对由 wditypes.hpp 或 dot11wdi.h 公开原始类型的引用。 使用默认序列化程序 (memcpy)，因此使用您自己承担，因为填充问题。

### <a name="attributes"></a>特性

-   `name` -父结构中的结构的名称。
-   `type` 若要在实际代码中使用的类型名称。
-   `description` – 结构使用友好说明。

### <a name="content"></a>内容

无。

### <a name="example"></a>示例

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


许多不同的容器的 TLV 容器。 这用于处理嵌套的 TLVs。

### <a name="attributes"></a>特性

-   `name` -ID 是所引用的 WDI 消息 / 其他容器。
-   `description` – 容器适用友好说明。
-   `type` 若要向代码公开的类型名称。

### <a name="content"></a>内容

列出的`<containerRef />`。

### <a name="example"></a>示例

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


描述所有容器中使用的所有结构。 也可以通过使用结构`<container />`，或由另一个引用`<propertyGroup />`（嵌套结构）。 它们独立于 TLVs 容器定义以便它们可以重新使用。 他们不具备 TLV 标头。

这些定义是必要的因为它们能帮您解决填充结构问题，并提供有关如何解释数据的代码生成器的说明。

**请注意**  此处顺序非常重要。 所有数据偏移量隐都式基于属性组描述，并且数据在此处定义的顺序写入/分析。 这些结构必须在此处定义。

 

## <a name="primitive-field-types-bool-uint8-uint16-uint32-int8-int16-int32"></a>基元字段类型 (`<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`)


这些是可用的基元类型，并将转换/封送适当地通过生成的代码。

### <a name="attributes"></a>特性

-   `name` 的父结构中字段名称。
-   `description` – 该属性是为友好说明。
-   `count` -多少有的给定属性。 默认值为 1。 大于 1 的值使此属性成为代码中以静态方式大小的数组。

### <a name="contents"></a>目录

无

## `<propertyGroup />`


单个的结构。

### <a name="attributes"></a>特性

-   `name` -ID 是所引用的 WDI 消息 / 其他容器。
-   `description` – 属性组是为友好说明。
-   `type` 若要向代码公开的类型名称。

### <a name="contents"></a>目录

有几种可能的属性类型 （结构字段）。

-   `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`

-   `<groupRef />`

-   `<namedType />`

### <a name="example"></a>示例

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

 

 





