---
title: MSFC\_FibrePortNPIVAttributes WMI 类
description: MSFC\_FibrePortNPIVAttributes WMI 类
ms.assetid: A778E00A-476C-4763-B652-3312B7913F9C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a35aa5a94f30d268eb28b510d6ba1d2a2d2352d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826135"
---
# <a name="msfc_fibreportnpivattributes-wmi-class"></a>MSFC\_FibrePortNPIVAttributes WMI 类


WMI 客户端使用 MSFC\_FibrePortNPIVAttributes 类来检索有关为物理端口创建的虚拟端口的信息。

*Npivwmi*中的 MSFC\_FibrePortNPIVAttributes 类定义如下：

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

[**MSFC\_FibrePortNPIVAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_fibreportnpivattributes)

没有与此 WMI 类相关联的方法。

 

 





