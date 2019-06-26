---
title: SCSI\_ADDR WMI 类
description: SCSI\_ADDR WMI 类
ms.assetid: 720cf803-b004-4c63-8884-66b0e07d82c0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 426eaa6a7ec68dae4b86ed79391baf2391244a63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384330"
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

此类定义编译时通过 WMI 工具套件，它会生成[ **SCSI\_ADDR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_scsi_addr)数据结构。 没有与此 WMI 类相关联的方法。

 

 





