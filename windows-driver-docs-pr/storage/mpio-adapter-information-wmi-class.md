---
title: MPIO\_适配器\_信息 WMI 类
description: MPIO\_适配器\_信息 WMI 类
ms.assetid: 748205a5-d37b-4080-b6ce-9176139cef4a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8616dd4021da05b66fee64b940a6a3e9f93716ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339592"
---
# <a name="mpioadapterinformation-wmi-class"></a>MPIO\_适配器\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_适配器\_信息 WMI 类，以标识与 MPIO 磁盘相关联的路径。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_适配器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562313)数据结构。 没有与此 WMI 类相关联的方法。

 

 





