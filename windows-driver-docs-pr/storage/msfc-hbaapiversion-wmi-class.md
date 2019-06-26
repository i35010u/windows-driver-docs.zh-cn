---
title: MSFC\_HbaApiVersion WMI 类
description: MSFC\_HbaApiVersion WMI 类
ms.assetid: 642b8313-d1ca-4c07-9c39-b49ef65b4438
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4a97e2579f71f20e8f26999eb97d26f356e81915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384152"
---
# <a name="msfchbaapiversion-wmi-class"></a>MSFC\_HbaApiVersion WMI 类


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 MSFC\_HbaApiVersion 类可以报告当前支持的 HBA API 版本。

MSFC\_HbaApiVersion 类定义中，如下所示*Hbaapi.mof*:

```cpp
class MSFC_HbaApiVersion
{
    uint32 WmiHbaApiVersion;
    uint32 HbaApiVersion;
    string Description;
};
```

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MSFC\_HbaApiVersion**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff562507(v=vs.85))

没有与此 WMI 类相关联的方法。

 

 





