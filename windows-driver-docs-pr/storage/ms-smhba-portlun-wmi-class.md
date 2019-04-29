---
title: MS\_SMHBA\_PORTLUN WMI 类
description: MS\_SMHBA\_PORTLUN WMI 类
ms.assetid: 28473b3b-2b88-4abc-81b5-9a6a7f8166e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 70a07917f4065bad385ff2966d676ddf6a111c7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380321"
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

[**MS\_SMHBA\_PORTLUN**](https://msdn.microsoft.com/library/windows/hardware/ff563169)

没有与此 WMI 类相关联的方法。

 

 





