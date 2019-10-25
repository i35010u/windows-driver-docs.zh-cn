---
title: MPIO\_驱动器\_信息 WMI 类
description: MPIO\_驱动器\_信息 WMI 类
ms.assetid: 4c116157-5f5b-4213-abdd-9128ebbfa341
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7631991eb53566830951fc83c480b19c3de7afb9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844974"
---
# <a name="mpio_drive_info-wmi-class"></a>MPIO\_驱动器\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_驱动器\_信息 WMI 类来标识它所管理的系统上的每个 MPIO 磁盘。

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

当 WMI 工具套件编译此类定义时，它将生成[**MPIO\_驱动器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_drive_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





