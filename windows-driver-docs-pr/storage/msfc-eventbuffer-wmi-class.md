---
title: MSFC \_ EVENTBUFFER WMI 类
description: MSFC \_ EVENTBUFFER WMI 类
ms.assetid: ce16e42c-5d0b-47e9-9baa-53dcec482940
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d1b8b19eb8ee3a84e35ba35a07124147f45ad7e2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184203"
---
# <a name="msfc_eventbuffer-wmi-class"></a>MSFC \_ EVENTBUFFER WMI 类


## <span id="ddk_msfc_eventbuffer_wmi_class_kr"></span><span id="DDK_MSFC_EVENTBUFFER_WMI_CLASS_KR"></span>


支持 T11 委员会 *光纤通道 HBA API* 规范的 hba 微型端口驱动程序使用 MSFC \_ EventBuffer 类将适配器事件数据报告给已注册为通知这些事件的 WMI 客户端。

MSFC \_ EventBuffer 类在 *Hbaapi*中定义如下：

```cpp
class MSFC_EventBuffer { 
  [WmiDataId(1)] uint32  EventType;
  [WmiDataId(2)] uint32  EventInfo[4];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ EventBuffer**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

没有与此 WMI 类相关联的方法。

 

