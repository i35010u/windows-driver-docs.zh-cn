---
title: MS \_ SMHBA \_ SCSIENTRY WMI 类
description: MS \_ SMHBA \_ SCSIENTRY WMI 类
ms.assetid: 8ac7a979-b3fe-4da6-a8e7-301c64b27e46
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e4060daa195858c931e2b733c7d73257651231c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193195"
---
# <a name="ms_smhba_scsientry-wmi-class"></a>MS \_ SMHBA \_ SCSIENTRY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ SCSIENTRY 类存储由操作系统生成的、用于唯一标识 SCSI 逻辑单元及其适配器的信息。 此类用于在操作系统信息与逻辑单元的 SSP 标识符之间构造绑定。

MS \_ SMHBA \_ SCSIENTRY 类在 *Hbaapi*中定义如下：

```cpp
class MS_SMHBA_SCSIENTRY
{
    [HBAType("MS_SMHBA_PORTLUN"), WmiDataId(1)]
    MS_SMHBA_PORTLUN PortLun;

    [HBAType("HBA_LUID"), WmiDataId(2)]
    uint8  LUID[256];

    [HBAType("HBA_SCSIID"), WmiDataId(3)]
    HBAScsiID ScsiId;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS \_ SMHBA \_ SCSIENTRY**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_scsientry)

没有与此 WMI 类相关联的方法。

 

