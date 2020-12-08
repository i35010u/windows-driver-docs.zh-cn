---
title: MPIO \_ 控制器 \_ 信息 WMI 类
description: MPIO \_ 控制器 \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 666e1c22aaeb3e1d5834be298ec71744b749dddc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835033"
---
# <a name="mpio_controller_info-wmi-class"></a>MPIO \_ 控制器 \_ 信息 WMI 类


MPIO 驱动程序使用 MPIO \_ 控制器 \_ 信息 WMI 类标识存储控制器及其关联的 DSM。

```cpp
class MPIO_CONTROLLER_INFO
{

    //
    // Devices behind this controller will have a matching
    // ControllerId in the PDO_INFORMATION class.
    //
    [WmiDataId(1)] uint32 IdentifierType;
    [WmiDataId(2)] uint32 IdentifierLength;
    [WmiDataId(3)] uint8 Identifier[32];
    [WmiDataId(4)] uint32 ControllerState;
    [WmiDataId(5)] uint32 Pad;
    [WmiDataId(6), MaxLen(63)] string AssociatedDsm;
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 控制器 \_ 信息**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_controller_info) 数据结构。 没有与此 WMI 类相关联的方法。

 

