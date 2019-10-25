---
title: SCSI\_地址 WMI 类
description: SCSI\_地址 WMI 类
ms.assetid: 720cf803-b004-4c63-8884-66b0e07d82c0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b1cdb41bff2866d0eab081d3f4b0cd227738eae5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842683"
---
# <a name="scsi_addr-wmi-class"></a>SCSI\_地址 WMI 类


MPIO 驱动程序使用 SCSI\_地址 WMI 类识别 MPIO 磁盘的 SCSI 地址。

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

当 WMI 工具套件编译此类定义时，它将生成[ **\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_scsi_addr)数据结构的 SCSI。 没有与此 WMI 类相关联的方法。

 

 





