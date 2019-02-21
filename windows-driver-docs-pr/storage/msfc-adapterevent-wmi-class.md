---
title: MSFC\_AdapterEvent WMI 类
description: MSFC\_AdapterEvent WMI 类
ms.assetid: 83077288-e3f6-4b21-80ed-677aad7d2979
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0218dfb72fb0cac509ed9debbefc96982af765fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519117"
---
# <a name="msfcadapterevent-wmi-class"></a>MSFC\_AdapterEvent WMI 类


## <span id="ddk_msfc_adapterevent_wmi_class_kr"></span><span id="DDK_MSFC_ADAPTEREVENT_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 MSFC\_AdapterEvent 类要报告给 WMI 客户端，以便将已注册的适配器事件的特征接收这些事件通知。

MSFC\_AdapterEvent 类定义中，如下所示*Hbaapi.mof*:

```cpp
class MSFC_AdapterEvent : WMIEvent  {
  [key] string InstanceName; boolean  Active;
  [WmiDataId(1), Description("Event Type") : amended, 
    _TYPE_QUALIFIERS] uint32  EventType;
  [WmiDataId(2), Description("Adapter WWN") : amended, 
    ("HBA_WWN")] uint8  PortWWN[8];
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_AdapterEvent**](https://msdn.microsoft.com/library/windows/hardware/ff562475)

没有与此 WMI 类相关联的方法。

 

 





