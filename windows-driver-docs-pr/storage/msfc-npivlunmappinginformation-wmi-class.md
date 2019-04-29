---
title: MSFC\_NPIVLUNMappingInformation WMI 类
description: MSFC\_NPIVLUNMappingInformation WMI 类
ms.assetid: F8BCDEDE-5EF3-464D-8592-5DF1878D3694
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 20e940d23502c8184a92b1575b995e3e0f065955
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378971"
---
# <a name="msfcnpivlunmappinginformation-wmi-class"></a>MSFC\_NPIVLUNMappingInformation WMI 类


WMI 客户端使用 MSFC\_LUNMappingInformation 类检索到的虚拟端口映射信息的 LUN。

MSFC\_NPIVLUNMappingInformation 类定义中，如下所示*Npivwmi.mof*:

```mof
class MSFC_NPIVLUNMappingInformation  
{  
    [WmiDataId(1), Description("The world wide port name of the virtual port"):Amended]  
     uint8 WWPNVirtualPort[8];  
  
    [WmiDataId(2), Description("The world wide port name of the physical port"):Amended]  
    uint8 WWPNPhysicalPort[8];  
  
    [WmiDataId(3),  
    read  
    ] uint8 OSBus;  
  
    [WmiDataId(4),  
    read  
    ] uint8 OSTarget;  
  
    [WmiDataId(5),  
    read  
    ] uint8 OSLUN;  
};  
```

编译时通过 WMI 工具套件，此类定义将生成以下数据结构：

[**MSFC\_NPIVLUNMappingInformation**](https://msdn.microsoft.com/library/windows/hardware/hh127626)

没有与此 WMI 类相关联的方法。

 

 





