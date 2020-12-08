---
title: PDOSCSI \_ 地址 WMI 类
description: PDOSCSI \_ 地址 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b720a869a3ced3188dfad1bf2a2ff20ad6147d1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792583"
---
# <a name="pdoscsi_addr-wmi-class"></a>PDOSCSI \_ 地址 WMI 类


MPIO 驱动程序使用 PDOSCSI \_ 地址 WMI 类识别物理设备的 SCSI 地址。

```cpp
class PDOSCSI_ADDR
{
    //
    // ScsiAddress: Port, Bus, Target, Lun
    //
    [WmiDataId(1)] uint8 PortNumber;
    [WmiDataId(2)] uint8 ScsiPathId;
    [WmiDataId(3)] uint8 TargetId;
    [WmiDataId(4)] uint8 Lun;
};
```

当 WMI 工具套件 iscompiled 此类定义时，它将生成 [**PDOSCSI \_ 地址**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_pdoscsi_addr) 数据结构。 没有与此 WMI 类相关联的方法。

 

