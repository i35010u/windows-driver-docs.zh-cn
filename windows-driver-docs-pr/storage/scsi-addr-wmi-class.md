---
title: SCSI\_ADDR WMI 类
description: SCSI\_ADDR WMI 类
ms.assetid: 720cf803-b004-4c63-8884-66b0e07d82c0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d50391a3f01b3ad6a3265bb0f3f8af5d8749950a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566957"
---
# <a name="scsiaddr-wmi-class"></a>SCSI\_ADDR WMI 类


MPIO 驱动程序使用 SCSI\_ADDR WMI 类，以标识 MPIO 磁盘的 SCSI 地址。

```cpp
class SCSI_ADDR
{
    //
    // ScsiAddress: Port, Bus, Target, Lun
    //
    [WmiDataId(1)] uint8 PortNumber;
    [WmiDataId(2)] uint8 ScsiPathId;
    [WmiDataId(3)] uint8 TargetId;
    [WmiDataId(4)] uint8 Lun;
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **SCSI\_ADDR** ](https://msdn.microsoft.com/library/windows/hardware/ff564952)数据结构。 没有与此 WMI 类相关联的方法。

 

 





