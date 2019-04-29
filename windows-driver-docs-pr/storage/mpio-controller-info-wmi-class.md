---
title: MPIO\_控制器\_信息 WMI 类
description: MPIO\_控制器\_信息 WMI 类
ms.assetid: 0448e056-2bbe-4e4f-a729-a872393222e5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 81e51f737eb560c3ba18a27f7faf070468961792
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391431"
---
# <a name="mpiocontrollerinfo-wmi-class"></a>MPIO\_控制器\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_控制器\_信息 WMI 类，以标识存储控制器和其关联的 DSM。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_控制器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562329)数据结构。 没有与此 WMI 类相关联的方法。

 

 





