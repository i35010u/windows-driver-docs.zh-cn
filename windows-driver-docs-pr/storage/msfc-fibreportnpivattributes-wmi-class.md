---
title: MSFC\_FibrePortNPIVAttributes WMI 类
description: MSFC\_FibrePortNPIVAttributes WMI 类
ms.assetid: A778E00A-476C-4763-B652-3312B7913F9C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 490b802bd1634ecb60b2733321c4c54a5b54c6b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362271"
---
# <a name="msfcfibreportnpivattributes-wmi-class"></a>MSFC\_FibrePortNPIVAttributes WMI 类


WMI 客户端使用 MSFC\_FibrePortNPIVAttributes 类用于检索有关为物理端口创建的虚拟端口的信息。

MSFC\_FibrePortNPIVAttributes 类定义中，如下所示*Npivwmi.mof*:

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

编译时通过 WMI 工具套件，此类定义将生成以下数据结构：

[**MSFC\_FibrePortNPIVAttributes**](https://msdn.microsoft.com/library/windows/hardware/hh127623)

没有与此 WMI 类相关联的方法。

 

 





