---
title: PDO \_ 信息 WMI 类
description: PDO \_ 信息 WMI 类
ms.assetid: 1a972905-42ea-4cb2-b937-5ed0f287d80a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 22529bb009e689e927a7022457bb817ed1dd3d07
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184387"
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

 

