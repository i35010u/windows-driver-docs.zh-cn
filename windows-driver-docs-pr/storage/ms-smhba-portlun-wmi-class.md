---
title: MS\_SMHBA\_PORTLUN WMI 类
description: MS\_SMHBA\_PORTLUN WMI 类
ms.assetid: 28473b3b-2b88-4abc-81b5-9a6a7f8166e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d99a4f2e3ad2cd8e98a22610e09f597ef014ed97
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386130"
---
# <a name="mssmhbaportlun-wmi-class"></a>MS\_SMHBA\_PORTLUN WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_PORTLUN 类公开的目标 LUN 和 SAS 适配器之间的映射。

MS\_SMHBA\_PORTLUN 类定义，如下所示在*Hbaapi.mof*:

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

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_PORTLUN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_portlun)

没有与此 WMI 类相关联的方法。

 

 





