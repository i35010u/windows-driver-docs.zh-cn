---
title: MSFC \_ FIBREPORTNPIVATTRIBUTES WMI 类
description: MSFC \_ FIBREPORTNPIVATTRIBUTES WMI 类
ms.assetid: A778E00A-476C-4763-B652-3312B7913F9C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dd270a3966ba4aa10b5042c482db80369c1158a7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184077"
---
# <a name="msfc_fibreportnpivattributes-wmi-class"></a>MSFC \_ FIBREPORTNPIVATTRIBUTES WMI 类


WMI 客户端使用 MSFC \_ FibrePortNPIVAttributes 类来检索有关为物理端口创建的虚拟端口的信息。

MSFC \_ FibrePortNPIVAttributes 类在 *Npivwmi*中定义如下：

```mof
class MSFC_FibrePortNPIVAttributes   
{  
    [WmiDataId(1), Description("The world wide port name of the physical port"):Amended]  
     uint8 WWPN[8];   
  
    [WmiDataId(2), Description("The world wide node name of the physical port"):Amended]  
     uint8 WWNN[8];   
  
    [WmiDataId(3),  
     read,  
     Description("Number of virtual ports on this adapter."):Amended  
    ]uint32 NumberVirtualPorts;  
  
     [WmiDataId(4),  
      read,  
      Description("Array of virtual ports."):Amended,
      WmiSizeIs("NumberVirtualPorts")  
     ]  
     MSFC_VirtualFibrePortAttributes VirtualPorts[];  
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ FibrePortNPIVAttributes**](/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_fibreportnpivattributes)

没有与此 WMI 类相关联的方法。

 

