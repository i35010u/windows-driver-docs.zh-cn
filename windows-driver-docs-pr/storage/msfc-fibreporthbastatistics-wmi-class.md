---
title: MSFC\_FibrePortHBAStatistics WMI 类
description: MSFC\_FibrePortHBAStatistics WMI 类
ms.assetid: 24c787b6-b9f7-4c9b-8d1d-6b2796f65622
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 91e67801cd058a2cd88a8a8dac3b3f0c32d0bbb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826163"
---
# <a name="msfc_fibreporthbastatistics-wmi-class"></a>MSFC\_FibrePortHBAStatistics WMI 类


## <span id="ddk_msfc_fibreporthbastatistics_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBASTATISTICS_WMI_CLASS_KR"></span>


WMI 客户端使用 MSFC\_FibrePortHBAStatistics 类来查询 HBA 微型端口驱动程序，以获取与 HBA 上端口相关的统计信息。 MSFC\_FibrePortHBAStatistics 类报告[MSFC\_HBAPORTSTATISTICS WMI 类](msfc-hbaportstatistics-wmi-class.md)中的所有信息，以及端口的一些标识符信息。

*Hbaapi*中的 MSFC\_FibrePortHBAStatistics 类定义如下：

```cpp
class MSFC_FibrePortHBAStatistics
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Description ("Unique identifier for the port. "
                   "This identifier must be unique "
                   "among all ports on all adapters."
                   "The same value for the identifier "
                   "must be used for the same port "
                   "in other classes that expose port "
                   "information") : amended,
     WmiRefClass("MSFC_FibrePort"),
     WmiRefProperty("UniquePortId"),
     WmiDataId(1)
    ]
    uint64 UniquePortId;
    [WmiDataId(2),
     HBA_STATUS_QUALIFIERS
    ]
    uint32 HBAStatus;
    // Note 4 byte padding
    [ WmiDataId(3) ]
    MSFC_HBAPortStatistics Statistics;
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC\_FibrePortHBAStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fibreporthbastatistics)

没有与此 WMI 类相关联的方法。

 

 





