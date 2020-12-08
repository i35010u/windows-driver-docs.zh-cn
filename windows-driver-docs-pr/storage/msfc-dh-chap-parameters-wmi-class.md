---
title: MSFC \_ DH \_ CHAP \_ 参数 WMI 类
description: MSFC \_ DH \_ CHAP \_ 参数 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b37d77a931b9105d9926150bea3f1c1cb83320fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811489"
---
# <a name="msfc_dh_chap_parameters-wmi-class"></a>MSFC \_ DH \_ CHAP \_ 参数 WMI 类


WMI 客户端使用 **MSFC \_ DH \_ Chap \_ Parameters** 类为虚拟端口上的 Chap 质询设置响应参数。

**MSFC \_ DH \_ Chap \_ 参数** 类在 *Npivwmi* 中定义如下：

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

由 WMI 工具套件编译时，此类定义生成以下数据结构：

**MSFC \_ DH \_ Chap \_ 参数**

没有与此 WMI 类相关联的方法。

 

 





