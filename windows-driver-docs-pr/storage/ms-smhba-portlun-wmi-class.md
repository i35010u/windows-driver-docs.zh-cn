---
title: MS \_ SMHBA \_ PORTLUN WMI 类
description: MS \_ SMHBA \_ PORTLUN WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9231fda008f1c8fc585750601d432c3ce3fabdee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785577"
---
# <a name="ms_smhba_portlun-wmi-class"></a>MS \_ SMHBA \_ PORTLUN WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ PORTLUN 类来公开目标 LUN 与 SAS 适配器之间的映射。

MS \_ SMHBA \_ PORTLUN 类在 *Hbaapi* 中定义如下：

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

 

