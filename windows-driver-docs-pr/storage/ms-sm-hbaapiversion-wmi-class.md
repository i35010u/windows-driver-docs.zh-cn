---
title: MS\_SM\_HbaApiVersion WMI 类
description: MS\_SM\_HbaApiVersion WMI 类
ms.assetid: 3d0591e5-ed95-4509-bd27-e122ac9186d2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d3b3fa51a7a9477a68c61ef32bd7f233c16b552
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323247"
---
# <a name="mssmhbaapiversion-wmi-class"></a>MS\_SM\_HbaApiVersion WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SM\_HbaApiVersion 类可以报告当前 HBA API 版本。

MS\_SM\_HbaApiVersion 类定义，如下所示在*Hbaapi.mof*:

```cpp
class MS_SM_HbaApiVersion
{
    uint32 WmiHbaApiVersion;  
    uint32 HbaApiVersion;  
    string Description;
};
```

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SM\_HbaApiVersion**](https://msdn.microsoft.com/library/windows/hardware/ff563211)

没有与此 WMI 类相关联的方法。

 

 





