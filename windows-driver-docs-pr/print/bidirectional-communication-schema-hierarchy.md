---
title: 双向通信架构层次结构
description: 双向通信架构层次结构
ms.assetid: b3435c17-f72b-4925-8d13-bd3e71b4947e
keywords:
- 双向通信架构 WDK 打印
- 双向通信架构 WDK 打印
- 层次结构 WDK bidi 通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17a038643a66fabf8374255195d22fd1ffa909d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379043"
---
# <a name="bidirectional-communication-schema-hierarchy"></a>双向通信架构层次结构

双向通信架构包含以下层次结构或树中的属性和值。

-   在纯文本 (例如，DeviceInfo) 中显示属性。

-   从 bidi 映射文件生成的属性显示在方括号中 (例如，\[类型\])。

-   斜体文本 (例如，FriendlyName) 中显示值。

```cpp
Printer
  DeviceInfo
 FriendlyName
 Manufacturer
 ModelName
 Location
    FirmwareVersion
    IEEE1284DeviceId
    NetworkingInfo
      HostName
      IPAddress
 Comment
  Configuration
    Memory
 Size
 PS
    HardDisk
 Installed
 Capacity
 FreeSpace
    DuplexUnit
 Installed
  Consumables
    [Name]
 Installed
      Type
      Color
      Level
      Model
  Layout
    NumberUp
      PagesPerSheet
 CurrentValue
 Supported
      Direction
 CurrentValue
 Supported
    Orientation
 CurrentValue
 Supported
    Resolution
 CurrentValue
 Supported
    InputBins
      [TrayName]
 Installed
 MediaSize
 MediaType
 MediaColor
 FeedDirection
 Capacity
 Level
  Finishing
 CollationSupported
 JogOffsetSupported
    Staple
 Installed
      Location
 CurrentValue
 Supported
      Angle
 CurrentValue
 Supported
    HolePunch
 Installed
      Pattern
 CurrentValue
 Supported
      Location
 CurrentValue
 Supported
    OutputBins
      [TrayName]
 Installed
 Capacity
 Level
Maintenance
    AlignHead
    CleanHead
Status
    Summary
 State
 StateReason
    Detailed
      Event###
 Name
        Component
 Group
 Name
 Severity
```

 

 




