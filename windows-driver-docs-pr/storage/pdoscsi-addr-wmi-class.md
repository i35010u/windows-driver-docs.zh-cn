---
title: PDOSCSI\_地址 WMI 类
description: PDOSCSI\_地址 WMI 类
ms.assetid: 8fdcfc5a-308a-457f-a015-e082e96f9df7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 99006f6a85f0561423cd8292501c532b13810531
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842731"
---
# <a name="pdoscsi_addr-wmi-class"></a>PDOSCSI\_地址 WMI 类


MPIO 驱动程序使用 PDOSCSI\_地址 WMI 类识别物理设备的 SCSI 地址。

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

如果此类定义由 WMI 工具套件 iscompiled，它将生成[**PDOSCSI\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_pdoscsi_addr)数据结构。 没有与此 WMI 类相关联的方法。

 

 





