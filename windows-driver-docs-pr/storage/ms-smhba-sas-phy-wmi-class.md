---
title: MS\_SMHBA\_SAS\_PHY WMI 类
description: MS\_SMHBA\_SAS\_PHY WMI 类
ms.assetid: c4fcf9ae-d2ab-4791-bf1e-55087fe03185
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b14290d44da932bdbed6346367693fad23da550
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386127"
---
# <a name="mssmhbasasphy-wmi-class"></a>MS\_SMHBA\_SAS\_PHY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_SAS\_PHY 类公开的关联的 SAS 端口的物理属性。 应为每个端口的此类的一个实例。

MS\_SMHBA\_SAS\_PHY 类定义，如下所示在*Hbaapi.mof*:

```cpp
class MS_SMHBA_SAS_PHY
{
    [WmiDataId(1)]
    uint8   PhyIdentifier;

    [WmiDataId(2), HBAType("HBA_SASPHYSPEED")]
    uint32  NegotiatedLinkRate;

    [WmiDataId(3), HBAType("HBA_SASPHYSPEED")]
    uint32  ProgrammedMinLinkRate;

    [WmiDataId(4), HBAType("HBA_SASPHYSPEED")]
    uint32  HardwareMinLinkRate;

    [WmiDataId(5), HBAType("HBA_SASPHYSPEED")]
    uint32  ProgrammedMaxLinkRate;

    [WmiDataId(6), HBAType("HBA_SASPHYSPEED")]
    uint32  HardwareMaxLinkRate;

    [WmiDataId(7), HBAType("HBA_WWN") ]
    uint8   domainPortWWN[8];
};
```

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_SAS\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_phy)

没有与此 WMI 类相关联的方法。

 

 





