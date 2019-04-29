---
title: WMI 类中的必需项
description: WMI 类中的必需项
ms.assetid: c978d8d0-5281-481a-b1e5-fd9a57d583d5
keywords:
- WDK WMI 类
- WMI WDK 内核类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 794cb1bfec53078ab31832c2af6adfa4ecd484b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324547"
---
# <a name="required-items-in-wmi-classes"></a>WMI 类中的必需项





所有类定义，但嵌入的类中必须包含项**InstanceName**和**Active**，它必须显示确切所示：

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

**InstanceName**并**Active**项是必需的并由 WMI 在内部使用。 驱动程序的数据和事件块的 MOF 类定义必须包含这些项，但该驱动程序必须响应查询的数据块或发送事件，因为它们不是驱动程序的数据块的一部分时未设置这些项。

 

 




