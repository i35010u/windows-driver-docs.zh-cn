---
title: MSFC \_ PORTEVENT WMI 类
description: MSFC \_ PORTEVENT WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 59f82d32338f37f8ef60fc908603ed011e8e8460
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785531"
---
# <a name="msfc_portevent-wmi-class"></a>MSFC \_ PORTEVENT WMI 类


## <span id="ddk_msfc_portevent_wmi_class_kr"></span><span id="DDK_MSFC_PORTEVENT_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC \_ PORTEVENT WMI 类来报告端口事件。

MSFC \_ PortEvent 类在 *Hbaapi* 中定义如下：

```cpp
class MSFC_PortEvent : WMIEvent {
  [key] 
  string InstanceName;
  boolean Active;
  [WmiDataId(1), Description("Type of event") : amended,
    EVENT_TYPES_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Fabric port id") : amended]
    uint32 FabricPortId;
  [WmiDataId(3), Description("Port WWN") : amended,
    HBAType("HBA_WWN")] uint8  PortWWN[8];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ PortEvent**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_portevent)

 

