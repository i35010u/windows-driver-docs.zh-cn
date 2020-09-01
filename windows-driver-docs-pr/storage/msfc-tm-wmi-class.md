---
title: MSFC \_ TM WMI 类
description: MSFC \_ TM WMI 类
ms.assetid: c81b9b2a-6381-4ff9-a579-bee53ac8678d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bf48f032f9ca8b39ac459a402ce9407306133cf8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184057"
---
# <a name="msfc_tm-wmi-class"></a>MSFC \_ TM WMI 类


## <span id="ddk_msfc_tm_wmi_class_kr"></span><span id="DDK_MSFC_TM_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC \_ TM WMI 类来时间戳事件。

MSFC \_ TM 类在 *Hbaapi*中定义如下：

```cpp
class MSFC_TM {
  [WmiDataId(1)] uint32  tm_sec;
  [WmiDataId(2)] uint32  tm_min;
  [WmiDataId(3)] uint32  tm_hour;
  [WmiDataId(4)] uint32  tm_mday;
  [WmiDataId(5)] uint32  tm_mon;
  [WmiDataId(6)] uint32  tm_year;
  [WmiDataId(7)] uint32  tm_wday;
  [WmiDataId(8)] uint32  tm_yday;
  [WmiDataId(9)] uint32  tm_isdst;
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ TM**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_tm)

 

