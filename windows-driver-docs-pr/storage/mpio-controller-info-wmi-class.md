---
title: MPIO\_控制器\_信息 WMI 类
description: MPIO\_控制器\_信息 WMI 类
ms.assetid: 0448e056-2bbe-4e4f-a729-a872393222e5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f272fccb05fb5599b4e24c82f295d55f1adfbddd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844546"
---
# <a name="mpio_controller_info-wmi-class"></a>MPIO\_控制器\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_控制器\_信息 WMI 类标识存储控制器及其关联的 DSM。

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

当 WMI 工具套件编译此类定义时，它将生成[**MPIO\_控制器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_controller_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





