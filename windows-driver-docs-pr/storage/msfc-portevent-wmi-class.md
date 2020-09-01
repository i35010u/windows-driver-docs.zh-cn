---
title: MSFC \_ PORTEVENT WMI 类
description: MSFC \_ PORTEVENT WMI 类
ms.assetid: 38b8e358-b118-4a0c-ac47-2f257d0ed1bf
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cb47fd99c0f4e3e21e04eb520dda4bee5a9e70be
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184675"
---
# <a name="msfc_portevent-wmi-class"></a>MSFC \_ PORTEVENT WMI 类


## <span id="ddk_msfc_portevent_wmi_class_kr"></span><span id="DDK_MSFC_PORTEVENT_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC \_ PORTEVENT WMI 类来报告端口事件。

MSFC \_ PortEvent 类在 *Hbaapi*中定义如下：

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

 

