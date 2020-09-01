---
title: MSFC \_ NPIVLUNMAPPINGINFORMATION WMI 类
description: MSFC \_ NPIVLUNMAPPINGINFORMATION WMI 类
ms.assetid: F8BCDEDE-5EF3-464D-8592-5DF1878D3694
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 35f5f7338a60c0f6f9397c9921bf94b5073cd4ea
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188503"
---
# <a name="msfc_npivlunmappinginformation-wmi-class"></a>MSFC \_ NPIVLUNMAPPINGINFORMATION WMI 类


WMI 客户端使用 MSFC \_ LUNMappingInformation 类将 LUN 检索到虚拟端口映射信息。

MSFC \_ NPIVLUNMappingInformation 类在 *Npivwmi*中定义如下：

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

 

