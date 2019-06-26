---
title: PDOSCSI\_ADDR WMI 类
description: PDOSCSI\_ADDR WMI 类
ms.assetid: 8fdcfc5a-308a-457f-a015-e082e96f9df7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 949ac7b6b472b24bc653b49726a2c72fb057fd72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382062"
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

当此类定义 iscompiled 按 WMI 工具套件，它会生成[ **PDOSCSI\_ADDR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_pdoscsi_addr)数据结构。 没有与此 WMI 类相关联的方法。

 

 





