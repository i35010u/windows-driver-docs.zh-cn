---
title: MSFC \_ VIRTUALFIBREPORTATTRIBUTES WMI 类
description: MSFC \_ VIRTUALFIBREPORTATTRIBUTES WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1a41960b5bfbba9a44c1a4fa184280fbb2164965
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811441"
---
# <a name="msfc_virtualfibreportattributes-wmi-class"></a>MSFC \_ VIRTUALFIBREPORTATTRIBUTES WMI 类


WMI 客户端使用 MSFC \_ VirtualFibrePortAttributes 类检索虚拟端口的属性。

MSFC \_ VirtualFibrePortAttributes 类在 *Npivwmi* 中定义如下：

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

 

