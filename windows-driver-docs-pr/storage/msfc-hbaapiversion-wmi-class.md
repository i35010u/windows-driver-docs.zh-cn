---
title: MSFC \_ HBAAPIVERSION WMI 类
description: MSFC \_ HBAAPIVERSION WMI 类
ms.assetid: 642b8313-d1ca-4c07-9c39-b49ef65b4438
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 902e38d36ccdabcf1290c6efe5935450a5ae4505
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188505"
---
# <a name="msfc_hbaapiversion-wmi-class"></a>MSFC \_ HBAAPIVERSION WMI 类


支持 T11 委员会 *光纤通道 HBA api* 规范的 hba 微型端口驱动程序使用 MSFC \_ HbaApiVersion 类来报告当前支持的 HBA API 版本。

MSFC \_ HbaApiVersion 类在 *Hbaapi*中定义如下：

```cpp
class MSFC_HbaApiVersion
{
    uint32 WmiHbaApiVersion;
    uint32 HbaApiVersion;
    string Description;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MSFC \_ HbaApiVersion**](/previous-versions/windows/hardware/drivers/ff562507(v=vs.85))

没有与此 WMI 类相关联的方法。

 

