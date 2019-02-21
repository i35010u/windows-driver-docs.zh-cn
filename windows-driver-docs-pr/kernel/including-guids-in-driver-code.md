---
title: 驱动程序代码中包括的 Guid
description: 驱动程序代码中包括的 Guid
ms.assetid: 9235f9e6-9c40-4c4b-a98b-99e6b46a11ce
keywords:
- 全局唯一标识符 WDK 内核
- Guid WDK 内核
- 标识符 WDK Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e083ae2ec3a89eb47292dafe80ca5705a0765a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524901"
---
# <a name="including-guids-in-driver-code"></a>驱动程序代码中包括的 Guid





若要在内核模式驱动程序中使用 Guid，必须执行两项操作：

1.  包含 Initguid.h 头文件，可重新定义**定义\_GUID**宏。

    Initguid.h 标头文件重新定义**定义\_GUID**宏来实例化 （而不只声明的外部引用） 的 Guid。 应实例化 Guid 在驱动程序源文件中包括此标头文件。 （用户模式应用程序包括 Objbase.h 包括标头文件包含 GUID 定义之前。）

2.  包含定义 Guid 的标头文件。

    语句后将 initguid.h 放，包括包含 GUID 定义这些标头文件。 驱动程序可能包括多个包含 GUID 定义，包括系统提供的标头文件和第三方头文件的标头文件。

下面的代码摘录显示了包括的 Guid 的语句的序列：

```cpp
:
// include system headers here such as wdm.h

#include <initguid.h>

// include system and driver-specific header files here that contain
// GUID definitions

...
```

将上述语句放在一个模块中的驱动程序;通常主模块。 当存在上述语句时，该驱动程序是指使用其符号名称的 GUID。








