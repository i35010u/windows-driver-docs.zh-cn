---
title: MS \_ SM \_ HbaApiVersion WMI 类
description: MS \_ SM \_ HbaApiVersion WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dfe90fbaf6216bb31a7d22c7cb6c83d8dc5c1749
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811529"
---
# <a name="ms_sm_hbaapiversion-wmi-class"></a>MS \_ SM \_ HbaApiVersion WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SM \_ HbaApiVersion 类报告当前 HBA API 版本。

MS \_ SM \_ HbaApiVersion 类在 *Hbaapi* 中定义如下：

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

 

