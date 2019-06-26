---
title: MSFC\_EventBuffer WMI 类
description: MSFC\_EventBuffer WMI 类
ms.assetid: ce16e42c-5d0b-47e9-9baa-53dcec482940
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e2e5d5d82aefc63473bdeda72ae1041f7a43f6cf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371162"
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

[**MSFC\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

没有与此 WMI 类相关联的方法。

 

 





