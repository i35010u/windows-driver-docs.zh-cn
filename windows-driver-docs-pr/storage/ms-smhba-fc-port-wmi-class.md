---
title: MS \_ SMHBA \_ FC \_ 端口 WMI 类
description: MS \_ SMHBA \_ FC \_ 端口 WMI 类
ms.assetid: 671f14e4-c591-4df2-85a1-2db3f802ef5e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7df1f53d398495b404d5125d890224f3a49a6ac1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188014"
---
# <a name="ms_smhba_fc_port-wmi-class"></a>MS \_ SMHBA \_ FC \_ 端口 WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ FC \_ 端口类公开关联 FC 适配器的端口属性。 每个端口都应有此类的一个实例。

\_ \_ 在 Hbaapi 中，MS SMHBA FC \_ 端口类定义如下*Hbaapi.mof*：

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

[**MS \_ SMHBA \_ FC \_ 端口**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_port)

没有与此 WMI 类相关联的方法。

 

