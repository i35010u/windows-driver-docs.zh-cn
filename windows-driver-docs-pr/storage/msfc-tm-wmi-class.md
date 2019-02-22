---
title: MSFC\_TM WMI 类
description: MSFC\_TM WMI 类
ms.assetid: c81b9b2a-6381-4ff9-a579-bee53ac8678d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 10f520f15b3e776ef6b40073a971359c5d22b391
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525950"
---
# <a name="msfctm-wmi-class"></a>MSFC\_TM WMI 类


## <span id="ddk_msfc_tm_wmi_class_kr"></span><span id="DDK_MSFC_TM_WMI_CLASS_KR"></span>


WMI 提供程序使用 MSFC\_到时间戳事件 TM WMI 类。

MSFC\_TM 类定义中，如下所示*Hbaapi.mof*:

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

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_TM**](https://msdn.microsoft.com/library/windows/hardware/ff562520)

 

 





