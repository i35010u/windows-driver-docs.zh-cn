---
title: MPIO \_ 驱动器 \_ 信息 WMI 类
description: MPIO \_ 驱动器 \_ 信息 WMI 类
ms.assetid: 4c116157-5f5b-4213-abdd-9128ebbfa341
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f27adbd0764139b43fb1c1e75eabeb20ef3a298a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193197"
---
# <a name="mpio_drive_info-wmi-class"></a>MPIO \_ 驱动器 \_ 信息 WMI 类


MPIO 驱动程序使用 MPIO \_ 驱动器 \_ 信息 WMI 类来标识它所管理的系统上的每个 MPIO 磁盘。

```cpp
class MPIO_DRIVE_INFO
{
    //
    // Number of Paths to the real device.
    //
    [WmiDataId(1)] uint32 NumberPaths;

    //
    // The MPIODisk(N).
    //
    [WmiDataId(2), MaxLen(63)] string Name;

    //
    // The real device's serial number.
    //
    [WmiDataId(3), MaxLen(63)] string SerialNumber;

    //
    // Friendly name of the DSM controlling the device.
    //
    [WmiDataId(4), MaxLen(63)] string DsmName;
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 驱动器 \_ 信息**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_drive_info) 数据结构。 没有与此 WMI 类相关联的方法。

 

