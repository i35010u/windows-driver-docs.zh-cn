---
title: MSFC\_TargetEvent WMI 类
description: MSFC\_TargetEvent WMI 类
ms.assetid: 251f7526-98e6-495d-a987-83257e968bb8
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7c2a9352ac2e59ae65a7d5cd60b1a4b9fb839b0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376725"
---
# <a name="msfctargetevent-wmi-class"></a>MSFC\_TargetEvent WMI 类


## <span id="ddk_msfc_targetevent_wmi_class_kr"></span><span id="DDK_MSFC_TARGETEVENT_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC\_TargetEvent WMI 类报告目标事件。

MSFC\_TargetEvent 类定义中，如下所示*Hbaapi.mof*:

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

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_TargetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_targetevent)

 

 





