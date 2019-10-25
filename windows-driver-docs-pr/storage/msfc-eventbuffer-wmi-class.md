---
title: MSFC\_EventBuffer WMI 类
description: MSFC\_EventBuffer WMI 类
ms.assetid: ce16e42c-5d0b-47e9-9baa-53dcec482940
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2926ab989023cf44656973b6bf888067e3cd037
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842867"
---
# <a name="msfc_eventbuffer-wmi-class"></a>MSFC\_EventBuffer WMI 类


## <span id="ddk_msfc_eventbuffer_wmi_class_kr"></span><span id="DDK_MSFC_EVENTBUFFER_WMI_CLASS_KR"></span>


支持 T11 委员会*光纤通道 HBA API*规范的 hba 微型端口驱动程序使用 MSFC\_EventBuffer 类将适配器事件数据报告给已注册为通知这些事件的 WMI 客户端。

*Hbaapi*中的 MSFC\_EventBuffer 类定义如下：

```cpp
class MSFC_EventBuffer { 
  [WmiDataId(1)] uint32  EventType;
  [WmiDataId(2)] uint32  EventInfo[4];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

没有与此 WMI 类相关联的方法。

 

 





