---
title: MSFC \_ TARGETEVENT WMI 类
description: MSFC \_ TARGETEVENT WMI 类
ms.assetid: 251f7526-98e6-495d-a987-83257e968bb8
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 50d1cbdd32bfc30ca13c8f8af2064dcbc1fc23e0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187801"
---
# <a name="msfc_targetevent-wmi-class"></a>MSFC \_ TARGETEVENT WMI 类


## <span id="ddk_msfc_targetevent_wmi_class_kr"></span><span id="DDK_MSFC_TARGETEVENT_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC \_ TARGETEVENT WMI 类来报告目标事件。

MSFC \_ TargetEvent 类在 *Hbaapi*中定义如下：

```cpp
class MSFC_TargetEvent : WmiEvent {
  [key] 
  string InstanceName;
  boolean Active;
  [WmiDataId(1), Description("Type of event") : amended,
    EVENT_TYPES_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Port WWN") : amended,
     HBAType("HBA_WWN")]uint8  PortWWN[8];
  [WmiDataId(3), Description("Discovered Port WWN") : amended,
    HBAType("HBA_WWN")]uint8  DiscoveredPortWWN[8];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ TargetEvent**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_targetevent)

 

