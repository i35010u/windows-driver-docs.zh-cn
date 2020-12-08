---
title: MSFC \_ NPIVLUNMAPPINGINFORMATION WMI 类
description: MSFC \_ NPIVLUNMAPPINGINFORMATION WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8e69a5948764680f205c2c97bb9a54dca379e690
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811457"
---
# <a name="msfc_npivlunmappinginformation-wmi-class"></a>MSFC \_ NPIVLUNMAPPINGINFORMATION WMI 类


WMI 客户端使用 MSFC \_ LUNMappingInformation 类将 LUN 检索到虚拟端口映射信息。

MSFC \_ NPIVLUNMappingInformation 类在 *Npivwmi* 中定义如下：

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

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ NPIVLUNMappingInformation**](/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_npivlunmappinginformation)

没有与此 WMI 类相关联的方法。

 

