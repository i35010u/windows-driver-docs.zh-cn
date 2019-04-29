---
title: PDOSCSI\_ADDR WMI 类
description: PDOSCSI\_ADDR WMI 类
ms.assetid: 8fdcfc5a-308a-457f-a015-e082e96f9df7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26957953dcf7a61a925390fffd07c4ede6757eb2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389419"
---
# <a name="pdoscsiaddr-wmi-class"></a>PDOSCSI\_ADDR WMI 类


MPIO 驱动程序使用 PDOSCSI\_ADDR WMI 类，以标识物理设备的 SCSI 地址。

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

当此类定义 iscompiled 按 WMI 工具套件，它会生成[ **PDOSCSI\_ADDR** ](https://msdn.microsoft.com/library/windows/hardware/ff563809)数据结构。 没有与此 WMI 类相关联的方法。

 

 





