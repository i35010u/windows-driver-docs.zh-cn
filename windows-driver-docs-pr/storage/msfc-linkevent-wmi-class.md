---
title: MSFC \_ LINKEVENT WMI 类
description: MSFC \_ LINKEVENT WMI 类
ms.assetid: 9507fb1a-ce2a-4ce9-8272-77c8c9d0a92c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8fc6252e864f2067f419ee53530d498823d62e1d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189249"
---
# <a name="msfc_linkevent-wmi-class"></a>MSFC \_ LINKEVENT WMI 类


## <span id="ddk_msfc_linkevent_wmi_class_kr"></span><span id="DDK_MSFC_LINKEVENT_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC \_ LINKEVENT WMI 类来报告链接事件。

MSFC \_ LinkEvent 类在 *Hbaapi*中定义如下：

```cpp
class MSFC_LinkEvent : WMIEvent {
  [key] 
  string InstanceName;
  boolean Active;
  [WmiDataId(1), Description("Type of event") : amended,
    EVENT_TYPES_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Discovered Port WWN") : amended,    HBAType("HBA_WWN")]uint8  AdapterWWN[8];
  [WmiDataId(3), Description("Size of RLIR buffer") : amended]
    uint32 RLIRBufferSize;
  [WmiDataId(4), Description("Size of RLIR buffer") : amended,
     WmiSizeIs("RLIRBufferSize")]uint8 RLIRBuffer[];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ LinkEvent**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_linkevent)

没有与此 WMI 类相关联的方法。

 

