---
title: MS\_SMHBA\_FC\_PHY WMI 类
description: MS\_SMHBA\_FC\_PHY WMI 类
ms.assetid: 8256eb6a-511f-4954-875e-755bd2bb3d65
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f8a03b6970ab4614904340403ffe2c7ec07fa768
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844538"
---
# <a name="ms_smhba_fc_phy-wmi-class"></a>MS\_SMHBA\_FC\_PHY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_FC\_PHY 类来公开关联 FC 端口的物理属性。 每个端口都应有此类的一个实例。

在*Hbaapi*中，MS\_SMHBA\_FC\_PHY 类定义如下：

```cpp
class MS_SMHBA_FC_PHY 
{
    [WmiDataId(1), HBAType("HBA_FCPHYSPEED")]
    uint32  PhySupportSpeed;

    [WmiDataId(2), HBAType("HBA_FCPHYSPEED")]
    uint32  PhySpeed;      

    [WmiDataId(3), HBAType("HBA_FCPHYTYPE")]
    uint8   PhyType;

    [WmiDataId(4)]
    uint32  MaxFrameSize; 
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS\_SMHBA\_FC\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_phy)

没有与此 WMI 类相关联的方法。

 

 





