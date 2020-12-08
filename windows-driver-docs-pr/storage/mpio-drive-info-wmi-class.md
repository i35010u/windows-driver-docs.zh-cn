---
title: MPIO \_ 驱动器 \_ 信息 WMI 类
description: MPIO \_ 驱动器 \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0789549769acd54438750f24feb2fafba8582d23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835025"
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

 

