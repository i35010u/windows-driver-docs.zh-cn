---
title: MPIO\_适配器\_信息 WMI 类
description: MPIO\_适配器\_信息 WMI 类
ms.assetid: 748205a5-d37b-4080-b6ce-9176139cef4a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 682e9b9793aeaf2b13d5c56db8acdef5c6502194
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844550"
---
# <a name="mpio_adapter_information-wmi-class"></a>MPIO\_适配器\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_适配器\_信息 WMI 类标识与 MPIO 磁盘关联的路径。

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

当 WMI 工具套件编译此类定义时，它将生成[**MPIO\_适配器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_adapter_information)数据结构。 没有与此 WMI 类相关联的方法。

 

 





