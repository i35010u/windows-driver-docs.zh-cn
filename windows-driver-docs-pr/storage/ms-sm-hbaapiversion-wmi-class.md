---
title: MS \_ SM \_ HbaApiVersion WMI 类
description: MS \_ SM \_ HbaApiVersion WMI 类
ms.assetid: 3d0591e5-ed95-4509-bd27-e122ac9186d2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d9ac92c0af7f2fcc0ae1d96ef044489301cb1582
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190625"
---
# <a name="ms_sm_hbaapiversion-wmi-class"></a>MS \_ SM \_ HbaApiVersion WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SM \_ HbaApiVersion 类报告当前 HBA API 版本。

MS \_ SM \_ HbaApiVersion 类在 *Hbaapi*中定义如下：

```cpp
class MS_SM_HbaApiVersion
{
    uint32 WmiHbaApiVersion;  
    uint32 HbaApiVersion;  
    string Description;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS \_ SM \_ HbaApiVersion**](/previous-versions/windows/hardware/drivers/ff563211(v=vs.85))

没有与此 WMI 类相关联的方法。

 

