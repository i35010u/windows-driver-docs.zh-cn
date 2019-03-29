---
title: MS\_SMHBA\_BINDINGENTRY WMI 类
description: MS\_SMHBA\_BINDINGENTRY WMI 类
ms.assetid: b7b2315f-21db-41a4-8390-3c413cb39f5b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f9dcb5d829ae0473fb41177da7060d0f66802be1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566448"
---
# <a name="mssmhbabindingentry-wmi-class"></a>MS\_SMHBA\_BINDINGENTRY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_BINDINGENTRY 类公开的 SSP 协议标识符和操作系统使用 SCSI 设备进行标识的数据之间的绑定信息设备。

MS\_SMHBA\_BINDINGENTRY 类 Hbaapi.mof 中定义，如下所示：

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

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

MS\_SMHBA\_BINDINGENTRY hbapiwmi.h 中找到。

没有与此 WMI 类相关联的方法。

 

 





