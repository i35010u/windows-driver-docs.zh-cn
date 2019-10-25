---
title: MS\_SMHBA\_SAS\_PHY WMI 类
description: MS\_SMHBA\_SAS\_PHY WMI 类
ms.assetid: c4fcf9ae-d2ab-4791-bf1e-55087fe03185
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8fceb02d1cf943250552d8136a26d977393dc65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844530"
---
# <a name="ms_smhba_sas_phy-wmi-class"></a>MS\_SMHBA\_SAS\_PHY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_SAS\_PHY 类公开关联 SAS 端口的物理属性。 每个端口都应有此类的一个实例。

在*Hbaapi*中，MS\_SMHBA\_SAS\_PHY 类定义如下：

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

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS\_SMHBA\_SAS\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_phy)

没有与此 WMI 类相关联的方法。

 

 





