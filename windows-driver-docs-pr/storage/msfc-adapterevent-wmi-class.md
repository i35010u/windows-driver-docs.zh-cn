---
title: MSFC \_ ADAPTEREVENT WMI 类
description: MSFC \_ ADAPTEREVENT WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 59332f683098ddb38f8d83089287b70f8f5c1a46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785566"
---
# <a name="msfc_adapterevent-wmi-class"></a>MSFC \_ ADAPTEREVENT WMI 类


## <span id="ddk_msfc_adapterevent_wmi_class_kr"></span><span id="DDK_MSFC_ADAPTEREVENT_WMI_CLASS_KR"></span>


支持 T11 委员会 *光纤通道 HBA API* 规范的 hba 微型端口驱动程序使用 MSFC \_ AdapterEvent 类将适配器事件的特征报告给已注册为通知这些事件的 WMI 客户端。

MSFC \_ AdapterEvent 类在 *Hbaapi* 中定义如下：

```cpp
class MSFC_AdapterEvent : WMIEvent  {
  [key] string InstanceName; boolean  Active;
  [WmiDataId(1), Description("Event Type") : amended, 
    _TYPE_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Adapter WWN") : amended, 
    ("HBA_WWN")] uint8  PortWWN[8];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ AdapterEvent**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_adapterevent)

没有与此 WMI 类相关联的方法。

 

