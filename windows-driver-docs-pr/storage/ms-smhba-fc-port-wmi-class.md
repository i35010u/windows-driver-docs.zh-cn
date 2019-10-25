---
title: MS\_SMHBA\_FC\_端口 WMI 类
description: MS\_SMHBA\_FC\_端口 WMI 类
ms.assetid: 671f14e4-c591-4df2-85a1-2db3f802ef5e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f1bc67601fcca2b7567e7d3800e767f9916f8a2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844536"
---
# <a name="ms_smhba_fc_port-wmi-class"></a>MS\_SMHBA\_FC\_端口 WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_FC\_端口类公开关联 FC 适配器的端口属性。 每个端口都应有此类的一个实例。

在*Hbaapi*中，MS\_SMHBA\_FC\_端口类定义如下：

```cpp
class MS_SMHBA_FC_Port 
{
    [HBAType("HBA_WWN"), WmiDataId(1)]
    uint8   NodeWWN[8];

    [HBAType("HBA_WWN"), WmiDataId(2)]
    uint8   PortWWN[8];

    [WmiDataId(3)]
    uint32  FcId;

    [HBAType("HBA_COS"), WmiDataId(4)]
    uint32  PortSupportedClassofService;

    [HBAType("HBA_FC4TYPES"), WmiDataId(5)]
    uint8   PortSupportedFc4Types[32];

    [HBAType("HBA_FC4TYPES"), WmiDataId(6)]
    uint8   PortActiveFc4Types[32];

    [HBAType("HBA_WWN"), WmiDataId(7)]
    uint8   FabricName[8];

    [WmiDataId(8)]
    uint32  NumberofDiscoveredPorts;

    [WmiDataId(9)] 
    uint8   NumberofPhys;

    [MaxLen(256), WmiDataId(10)]
    string  PortSymbolicName;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS\_SMHBA\_FC\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_port)

没有与此 WMI 类相关联的方法。

 

 





