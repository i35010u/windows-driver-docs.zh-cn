---
title: MSFC\_FibrePortHBAAttributes WMI 类
description: MSFC\_FibrePortHBAAttributes WMI 类
ms.assetid: 028afadf-1a2d-4792-8b6c-d53359af64c1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f7bccc0deca37b434610b4b82fa847a60c58dd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534883"
---
# <a name="msfcfibreporthbaattributes-wmi-class"></a>MSFC\_FibrePortHBAAttributes WMI 类


## <span id="ddk_msfc_fibreporthbaattributes_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBAATTRIBUTES_WMI_CLASS_KR"></span>


支持 FCbre 通道 HBA API HBA 微型端口驱动程序使用 MSFC\_FibrePortHBAAttributes WMI 类来公开与光纤通道端口相关联的属性信息。 应为每个端口的此类的一个实例。

MSFC\_FibrePortHBAAttributes 类定义中，如下所示*Hbaapi.mof*:

```cpp
class MSFC_FibrePortHBAAttributes {
  [key] 
  string InstanceName;
  boolean Active;
  [Description ("Unique identifier for the port. "
    "This identifier must be unique among all "
    "ports on all adapters. The same value for "
    "in other classes that expose port information"
    "the identifier must be used for the same port") : amended,
    WmiRefClass("MSFC_FibrePort"),
    WmiRefProperty("UniquePortId"),
    WmiDataId(1)
    ] uint64 UniquePortId;
  [HBA_STATUS_QUALIFIERS, WmiDataId(2)] HBA_STATUS  HBAStatus;
  [HBAType("HBA_PORTATTRIBUTES"),WmiDataId(3)]
    MSFC_HBAPortAttributesResults Attributes;
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_FibrePortHBAAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff562499)

没有与此 WMI 类相关联的方法。

 

 





