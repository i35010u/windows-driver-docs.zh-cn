---
title: MS \_ SMHBA \_ SAS \_ PHY WMI 类
description: MS \_ SMHBA \_ SAS \_ PHY WMI 类
ms.assetid: c4fcf9ae-d2ab-4791-bf1e-55087fe03185
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dcb979d7df306c2e1a7ae3baadfdb765bbd05def
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187797"
---
# <a name="ms_smhba_sas_phy-wmi-class"></a>MS \_ SMHBA \_ SAS \_ PHY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ SAS \_ PHY 类公开关联 SAS 端口的物理属性。 每个端口都应有此类的一个实例。

\_ \_ 在 Hbaapi 中，MS SMHBA SAS \_ PHY 类定义如下*Hbaapi.mof*：

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

[**MS \_ SMHBA \_ SAS \_ PHY**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_phy)

没有与此 WMI 类相关联的方法。

 

