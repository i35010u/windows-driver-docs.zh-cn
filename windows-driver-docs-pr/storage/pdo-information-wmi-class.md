---
title: PDO\_信息 WMI 类
description: PDO\_信息 WMI 类
ms.assetid: 1a972905-42ea-4cb2-b937-5ed0f287d80a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 30d92578d1ae17a72b5735647537ea50005f95d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389418"
---
# <a name="pdoinformation-wmi-class"></a>PDO\_信息 WMI 类


MPIO 驱动程序使用 PDO\_信息 WMI 类，以识别物理设备的设备路径映射。

```cpp
class PDO_INFORMATION
{

    [WmiDataId(1)] PDOSCSI_ADDR ScsiAddress;

    //
    // Indicates whether this device-path is usable,
    // i.e. whether DsmIsPathActive returned TRUE for this device-path.
    //
    [WmiDataId(2)] uint32 DeviceState;

    //
    // The PathId matches the identifier returned by DsmSetDeviceInfo.
    //
    [WmiDataId(3)] uint64 PathIdentifier;

    //
    // Matches the MPIO_CONTROLLER_INFO ControllerId of the controller
    // fronting this device.
    //
    [WmiDataId(4)] uint32 IdentifierType;
    [WmiDataId(5)] uint32 IdentifierLength;
    [WmiDataId(6)] uint8 Identifier[32];
    [WmiDataId(7)] uint8 Pad[4];
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **PDO\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563828)数据结构。 没有与此 WMI 类相关联的方法。

 

 





