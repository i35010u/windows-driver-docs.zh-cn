---
title: MSFC \_ VIRTUALFIBREPORTATTRIBUTES WMI 类
description: MSFC \_ VIRTUALFIBREPORTATTRIBUTES WMI 类
ms.assetid: D605D63F-0EBF-44C0-8ADE-729F2DE48487
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dce0c1d542fdc1de3449a6207e4aef9a19dea105
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192655"
---
# <a name="msfc_virtualfibreportattributes-wmi-class"></a>MSFC \_ VIRTUALFIBREPORTATTRIBUTES WMI 类


WMI 客户端使用 MSFC \_ VirtualFibrePortAttributes 类检索虚拟端口的属性。

MSFC \_ VirtualFibrePortAttributes 类在 *Npivwmi*中定义如下：

```mof
class MSFC_VirtualFibrePortAttributes  
{  
    [WmiDataId(1), Description("Status of the virtual port"):Amended,  
    uint32 Status;  
  
    [WmiDataId(2), Description("FC Id"):Amended]  
    uint32 FCId;  
      
    [WmiDataId(3), Description("Port symbolic name"):Amended]  
    uint16 VirtualName[64];  
  
    [WmiDataId(4), Description("An opaque tag passed in by the app. 128 bit so that a guid can be stored in it."):Amended]  
    uint8 Tag[16];  
  
    [WmiDataId(5), Description("The world wide port name of the virtual port"):Amended]  
    uint8 WWPN[8];   
  
    [WmiDataId(6), Description("The world wide node name of the virtual port"):Amended]  
    uint8 WWNN[8];   
  
    [WmiDataId(7), Description("The world wide node name of fabric"):Amended]  
    uint8 FabricWWN[8];  
};  
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ VirtualFibrePortAttributes**](/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_virtualfibreportattributes)

没有与此 WMI 类相关联的方法。

 

