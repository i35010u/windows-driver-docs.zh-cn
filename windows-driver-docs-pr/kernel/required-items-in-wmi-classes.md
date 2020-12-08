---
title: WMI 类中的必需项
description: WMI 类中的必需项
keywords:
- 类 WDK WMI
- WMI WDK 内核，类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7427d3d3f737957318c3f21234037c12c4b36e9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790507"
---
# <a name="required-items-in-wmi-classes"></a>WMI 类中的必需项





除嵌入类之外的所有类定义都必须包含项 **InstanceName** 和 **Active**，它们必须完全按所示显示：

```cpp
//WMI class definition
[
    //Class qualifiers
]
ClassName : BaseClassName
{
    [key, read]
     string InstanceName;
    [read] 
     boolean Active;
 
    // Driver-defined data items
}
```

**实例** 名称和 **活动** 项是必需的，并在内部由 WMI 使用。 驱动程序的数据和事件块的 MOF 类定义必须包含这些项，但驱动程序在响应数据块或发送事件的查询时不得设置这些项，因为它们不是驱动程序的数据块的一部分。

 

 




