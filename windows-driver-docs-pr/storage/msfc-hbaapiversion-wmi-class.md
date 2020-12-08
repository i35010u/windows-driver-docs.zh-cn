---
title: MSFC \_ HBAAPIVERSION WMI 类
description: MSFC \_ HBAAPIVERSION WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 740dc90a3c199a9abf2443f9daee9267a70af109
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785541"
---
# <a name="msfc_hbaapiversion-wmi-class"></a>MSFC \_ HBAAPIVERSION WMI 类


支持 T11 委员会 *光纤通道 HBA api* 规范的 hba 微型端口驱动程序使用 MSFC \_ HbaApiVersion 类来报告当前支持的 HBA API 版本。

MSFC \_ HbaApiVersion 类在 *Hbaapi* 中定义如下：

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

 

