---
title: MPIO \_ 适配器 \_ 信息 WMI 类
description: MPIO \_ 适配器 \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f0d7921d42da2e43f993804f4735e9f56b4eb6ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835041"
---
# <a name="mpio_adapter_information-wmi-class"></a>MPIO \_ 适配器 \_ 信息 WMI 类


MPIO 驱动程序使用 MPIO \_ 适配器 \_ 信息 WMI 类标识与 MPIO 磁盘关联的路径。

```cpp
class MPIO_ADAPTER_INFORMATION
{
    //
    // Path ID. The PDO_INFORMATION class includes
    // it's pathId. These values can be used to find
    // which devices are on which path.
    //
    [WmiDataId(1)] uint64 PathId;

    //
    // Adapter Location.
    //
    [WmiDataId(2)] uint8 BusNumber;
    [WmiDataId(3)] uint8 DeviceNumber;
    [WmiDataId(4)] uint8 FunctionNumber;
    [WmiDataId(5)] uint8 Pad;

    //
    // Adapter Name.
    //
    [WmiDataId(6), MaxLen(63)] string AdapterName;
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 适配器 \_ 信息**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_adapter_information) 数据结构。 没有与此 WMI 类相关联的方法。

 

