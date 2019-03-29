---
title: MPIO\_驱动器\_信息 WMI 类
description: MPIO\_驱动器\_信息 WMI 类
ms.assetid: 4c116157-5f5b-4213-abdd-9128ebbfa341
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7a1e4a6d443c172f88f49c7947e7bd1b920b2177
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349866"
---
# <a name="mpiodriveinfo-wmi-class"></a>MPIO\_驱动器\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_驱动器\_信息 WMI 类，以确定它所管理的系统上每个 MPIO 的磁盘。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_驱动器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562377)数据结构。 没有与此 WMI 类相关联的方法。

 

 





