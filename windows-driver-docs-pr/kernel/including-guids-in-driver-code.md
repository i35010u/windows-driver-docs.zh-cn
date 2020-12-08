---
title: 在驱动程序代码中包含 GUID
description: 在驱动程序代码中包含 GUID
keywords:
- 全局唯一标识符 WDK 内核
- Guid WDK 内核
- 标识符 WDK Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1ba5d68448f2a0d99b554b856ca3db1f1242edc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788639"
---
# <a name="including-guids-in-driver-code"></a>在驱动程序代码中包含 GUID





若要在内核模式驱动程序中使用 Guid，必须执行以下两项操作：

1.  包括重新 **定义定义 \_ GUID** 宏的 initguid.h 头文件。

    Initguid.h 头文件重新定义了 **定义 \_ guid** 宏来实例化 guid (而不是声明外部引用) 。 将此标头文件包含在应实例化 Guid 的驱动程序源文件中。  (用户模式应用程序包括 Objbase，然后才能包含包含 GUID 定义的标头文件。 ) 

2.  包括定义 Guid)  (的标头文件。

    在要包含 Initguid.h 的语句后，包括包含 GUID 定义的标头文件。 驱动程序可能包含多个包含 GUID 定义的标头文件，包括系统提供的标头文件和第三方标头文件。

以下代码摘录显示了包含 Guid 的语句的顺序：

```cpp
:
// include system headers here such as wdm.h

#include <initguid.h>

// include system and driver-specific header files here that contain
// GUID definitions

...
```

将以上语句放入驱动程序的一个模块中;通常是主模块。 如果出现上述语句，驱动程序将使用其符号名称引用 GUID。








