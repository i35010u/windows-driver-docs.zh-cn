---
title: PDO \_ 信息 WMI 类
description: PDO \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 01b77adb637478a39b711925dfc8880381d00c92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792595"
---
# <a name="pdo_information-wmi-class"></a>PDO \_ 信息 WMI 类


MPIO 驱动程序使用 PDO \_ 信息 WMI 类识别物理设备的设备到路径映射。

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

当 WMI 工具套件编译此类定义时，它将生成 [**PDO \_ 信息**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_pdo_information) 数据结构。 没有与此 WMI 类相关联的方法。

 

