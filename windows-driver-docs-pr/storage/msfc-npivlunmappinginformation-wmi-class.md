---
title: MSFC\_NPIVLUNMappingInformation WMI 类
description: MSFC\_NPIVLUNMappingInformation WMI 类
ms.assetid: F8BCDEDE-5EF3-464D-8592-5DF1878D3694
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 67a72fc8ba7a6f8005b3be662b2d96e35cd29ace
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376733"
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

[**MSFC\_NPIVLUNMappingInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/npivwmi/ns-npivwmi-_msfc_npivlunmappinginformation)

没有与此 WMI 类相关联的方法。

 

 





