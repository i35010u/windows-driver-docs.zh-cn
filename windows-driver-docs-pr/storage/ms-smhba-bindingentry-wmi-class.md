---
title: MS \_ SMHBA \_ BINDINGENTRY WMI 类
description: MS \_ SMHBA \_ BINDINGENTRY WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 364d3f76e27f9a15407382c0763c96419b53ea60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811509"
---
# <a name="ms_smhba_bindingentry-wmi-class"></a>MS \_ SMHBA \_ BINDINGENTRY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ BINDINGENTRY 类来公开操作系统用于标识 SCSI 设备的数据与设备的 SSP 协议标识符之间的绑定信息。

MS \_ SMHBA \_ BINDINGENTRY 类在 Hbaapi 中定义如下：

```cpp
class MS_SMHBA_BINDINGENTRY
{
    [SMHBA_BIND_TYPE_QUALIFIERS, WmiDataId(1)]
    uint32 type;

    [HBAType("MS_SMHBA_PORTLUN"), WmiDataId(2)]
    MS_SMHBA_PORTLUN  PortLun;

    [HBAType("HBA_LUID"), WmiDataId(3)]
    uint8  LUID[256];

    [HBA_STATUS_QUALIFIERS, WmiDataId(4)]
    HBA_STATUS Status;

    [HBAType("HBA_SCSIID"), WmiDataId(5)]
    HBAScsiID ScsiId;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

\_ \_ Hbapiwmi 中找到了 MS SMHBA BINDINGENTRY。

没有与此 WMI 类相关联的方法。

 

 





