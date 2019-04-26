---
title: MSFC\_DH\_Chap\_参数 WMI 类
description: MSFC\_DH\_Chap\_参数 WMI 类
ms.assetid: 259E3935-0F37-4DBE-BED3-C55A6715A810
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9cbe71379f0364f7521fe2752164d4a9d1a46b14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325295"
---
# <a name="msfcdhchapparameters-wmi-class"></a>MSFC\_DH\_Chap\_参数 WMI 类


WMI 客户端使用**MSFC\_DH\_Chap\_参数**类上的虚拟端口设置 CHAP 质询响应参数。

**MSFC\_DH\_Chap\_参数**，如下所示在定义类*Npivwmi.mof*:

```mof
class MSFC_DH_Chap_Parameters
{    
    [WmiDataId(1),
     Description("Length in bytes of the shared secret."):Amended]
    uint32 SharedSecretLength;
   
    [WmiDataId(2),
    Description("Shared Secret Encoding"):Amended,
     ValueMap {"1", "2"},
     Values {"Printable ASCII", "Binary"}]
    uint8 SecretEncoding;

    [WmiDataId(3),
     WmiSizeIs("SharedSecretLength"),
     Description("Shared secret to be used at the basis of a DH-CHAP challenge."):Amended]
    uint8 SharedSecret[];
};
```

编译时通过 WMI 工具套件，此类定义将生成以下数据结构：

**MSFC\_DH\_Chap\_参数**

没有与此 WMI 类相关联的方法。

 

 





