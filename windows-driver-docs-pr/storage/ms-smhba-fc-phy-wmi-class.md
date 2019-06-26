---
title: MS\_SMHBA\_FC\_PHY WMI 类
description: MS\_SMHBA\_FC\_PHY WMI 类
ms.assetid: 8256eb6a-511f-4954-875e-755bd2bb3d65
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c547d1132febbce0f215c65fdae8cf4f03bf46c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386136"
---
# <a name="mssmhbafcphy-wmi-class"></a>MS\_SMHBA\_FC\_PHY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_FC\_PHY 类公开相关联的光纤通道端口的物理属性。 应为每个端口的此类的一个实例。

MS\_SMHBA\_FC\_PHY 类定义，如下所示在*Hbaapi.mof*:

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

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_FC\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_phy)

没有与此 WMI 类相关联的方法。

 

 





