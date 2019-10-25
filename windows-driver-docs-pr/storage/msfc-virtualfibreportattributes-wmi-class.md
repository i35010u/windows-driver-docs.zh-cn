---
title: MSFC\_VirtualFibrePortAttributes WMI 类
description: MSFC\_VirtualFibrePortAttributes WMI 类
ms.assetid: D605D63F-0EBF-44C0-8ADE-729F2DE48487
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 34206f03a4fed727db95338b47d577eed4385164
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845597"
---
# <a name="msfc_virtualfibreportattributes-wmi-class"></a>MSFC\_VirtualFibrePortAttributes WMI 类


WMI 客户端使用 MSFC\_VirtualFibrePortAttributes 类检索虚拟端口的属性。

*Npivwmi*中的 MSFC\_VirtualFibrePortAttributes 类定义如下：

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

[**MSFC\_VirtualFibrePortAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/npivwmi/ns-npivwmi-_msfc_virtualfibreportattributes)

没有与此 WMI 类相关联的方法。

 

 





