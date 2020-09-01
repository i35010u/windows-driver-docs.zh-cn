---
title: PDOSCSI \_ 地址 WMI 类
description: PDOSCSI \_ 地址 WMI 类
ms.assetid: 8fdcfc5a-308a-457f-a015-e082e96f9df7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d9e1dfd7309b46ccb217c5a0ca3dce9c0b8c6d5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185107"
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

 

