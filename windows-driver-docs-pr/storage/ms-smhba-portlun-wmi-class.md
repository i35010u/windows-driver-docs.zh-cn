---
title: MS\_SMHBA\_PORTLUN WMI 类
description: MS\_SMHBA\_PORTLUN WMI 类
ms.assetid: 28473b3b-2b88-4abc-81b5-9a6a7f8166e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b5140605d22a058d1f29eb053dcf53ecdc0fcce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844544"
---
# <a name="ms_smhba_portlun-wmi-class"></a>MS\_SMHBA\_PORTLUN WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_PORTLUN 类来公开目标 LUN 与 SAS 适配器之间的映射。

MS\_SMHBA\_PORTLUN 类在*Hbaapi*中定义如下：

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

[**MS\_SMHBA\_PORTLUN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_portlun)

没有与此 WMI 类相关联的方法。

 

 





