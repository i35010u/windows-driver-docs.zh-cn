---
title: MSFC\_LinkEvent WMI 类
description: MSFC\_LinkEvent WMI 类
ms.assetid: 9507fb1a-ce2a-4ce9-8272-77c8c9d0a92c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5428809627f1e8a7559a192d9bf060fefea84fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554513"
---
# <a name="msfclinkevent-wmi-class"></a>MSFC\_LinkEvent WMI 类


## <span id="ddk_msfc_linkevent_wmi_class_kr"></span><span id="DDK_MSFC_LINKEVENT_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC\_LinkEvent WMI 类来报告链接事件。

MSFC\_LinkEvent 类定义中，如下所示*Hbaapi.mof*:

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

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_LinkEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562514)

没有与此 WMI 类相关联的方法。

 

 





