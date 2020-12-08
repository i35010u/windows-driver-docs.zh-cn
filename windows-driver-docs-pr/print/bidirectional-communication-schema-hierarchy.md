---
title: 双向通信架构层次结构
description: 双向通信架构层次结构
keywords:
- 双向通信架构 WDK 打印
- 双向通信架构 WDK 打印
- 层次结构 WDK 双向通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12efcb7eb4e9115e773b85347c67f9d381ecfdca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797811"
---
# <a name="bidirectional-communication-schema-hierarchy"></a>双向通信架构层次结构

双向通信架构包含下面的层次结构或属性和值树。

-   属性以纯文本形式显示 (例如 DeviceInfo) 。

-   从双向映射文件生成的属性将显示在括号中 (例如， \[ 键入 \]) 。

-   值以斜体文本显示 (例如，FriendlyName) 。

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

 

 




