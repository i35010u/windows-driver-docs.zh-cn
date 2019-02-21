---
title: MSFC\_EventBuffer WMI 类
description: MSFC\_EventBuffer WMI 类
ms.assetid: ce16e42c-5d0b-47e9-9baa-53dcec482940
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3665c95af6708bd9f0df839dbe42398d85c65adb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554529"
---
# <a name="msfceventbuffer-wmi-class"></a>MSFC\_EventBuffer WMI 类


## <span id="ddk_msfc_eventbuffer_wmi_class_kr"></span><span id="DDK_MSFC_EVENTBUFFER_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 MSFC\_EventBuffer 类将适配器事件数据报告给已注册的这些通知的 WMI 客户端事件。

MSFC\_EventBuffer 类定义中，如下所示*Hbaapi.mof*:

```cpp
class MSFC_EventBuffer { 
  [WmiDataId(1)] uint32  EventType;
  [WmiDataId(2)] uint32  EventInfo[4];
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_EventBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562480)

没有与此 WMI 类相关联的方法。

 

 





