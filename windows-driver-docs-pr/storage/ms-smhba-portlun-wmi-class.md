---
title: MS \_ SMHBA \_ PORTLUN WMI 类
description: MS \_ SMHBA \_ PORTLUN WMI 类
ms.assetid: 28473b3b-2b88-4abc-81b5-9a6a7f8166e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5397d2e20f8bc5338a83b8ccea5326d5fda11a11
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191121"
---
# <a name="ms_smhba_portlun-wmi-class"></a>MS \_ SMHBA \_ PORTLUN WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ PORTLUN 类来公开目标 LUN 与 SAS 适配器之间的映射。

MS \_ SMHBA \_ PORTLUN 类在 *Hbaapi*中定义如下：

```cpp
class MS_SMHBA_PORTLUN 
{
    [HBAType("HBA_WWN"), WmiDataId(1)]
    uint8   PortWWN[8];

    [HBAType("HBA_WWN"), WmiDataId(2)]
    uint8   domainPortWWN[8];

    [HBAType("HBA_SCSILUN"), WmiDataId(3)]
    uint64  TargetLun;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS \_ SMHBA \_ PORTLUN**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_portlun)

没有与此 WMI 类相关联的方法。

 

