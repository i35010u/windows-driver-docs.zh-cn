---
title: MSFC\_FibrePortHBAStatistics WMI 类
description: MSFC\_FibrePortHBAStatistics WMI 类
ms.assetid: 24c787b6-b9f7-4c9b-8d1d-6b2796f65622
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e333ed7bc83204f5ade7990b763937abe817a044
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380602"
---
# <a name="msfcfibreporthbastatistics-wmi-class"></a>MSFC\_FibrePortHBAStatistics WMI 类


## <span id="ddk_msfc_fibreporthbastatistics_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBASTATISTICS_WMI_CLASS_KR"></span>


WMI 客户端使用 MSFC\_FibrePortHBAStatistics 类，查询统计信息的 HBA 微型端口驱动程序与 HBA 上的端口。 MSFC\_FibrePortHBAStatistics 类报告中的信息的所有[MSFC\_HBAPortStatistics WMI 类](msfc-hbaportstatistics-wmi-class.md)以及端口某些标识符信息。

MSFC\_FibrePortHBAStatistics 类定义中，如下所示*Hbaapi.mof*:

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

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_FibrePortHBAStatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_fibreporthbastatistics)

没有与此 WMI 类相关联的方法。

 

 





