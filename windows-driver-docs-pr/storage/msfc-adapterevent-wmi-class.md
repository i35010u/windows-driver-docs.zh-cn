---
title: MSFC\_AdapterEvent WMI 类
description: MSFC\_AdapterEvent WMI 类
ms.assetid: 83077288-e3f6-4b21-80ed-677aad7d2979
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 616383dd556c31ed0508ac0edb4c30dfb0f54f6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844519"
---
# <a name="msfc_adapterevent-wmi-class"></a>MSFC\_AdapterEvent WMI 类


## <span id="ddk_msfc_adapterevent_wmi_class_kr"></span><span id="DDK_MSFC_ADAPTEREVENT_WMI_CLASS_KR"></span>


支持 T11 委员会*光纤通道 HBA API*规范的 hba 微型端口驱动程序使用 MSFC\_AdapterEvent 类将适配器事件的特征报告给已注册为通知这些事件的 WMI 客户端。

*Hbaapi*中的 MSFC\_AdapterEvent 类定义如下：

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

[**MSFC\_AdapterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_adapterevent)

没有与此 WMI 类相关联的方法。

 

 





