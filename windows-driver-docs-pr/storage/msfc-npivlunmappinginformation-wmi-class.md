---
title: MSFC\_NPIVLUNMappingInformation WMI 类
description: MSFC\_NPIVLUNMappingInformation WMI 类
ms.assetid: F8BCDEDE-5EF3-464D-8592-5DF1878D3694
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 62875ed4b850796bd6bc7d0918a5d3d0832e4c7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824257"
---
# <a name="msfc_npivlunmappinginformation-wmi-class"></a>MSFC\_NPIVLUNMappingInformation WMI 类


WMI 客户端使用 MSFC\_LUNMappingInformation 类将 LUN 检索到虚拟端口映射信息。

*Npivwmi*中的 MSFC\_NPIVLUNMappingInformation 类定义如下：

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

[**MSFC\_NPIVLUNMappingInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_npivlunmappinginformation)

没有与此 WMI 类相关联的方法。

 

 





