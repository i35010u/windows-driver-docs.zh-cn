---
title: C28152
description: 警告 C28152 DO_DEVICE_INITIALIZING 意外返回 AddDevice 函数。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28152
ms.openlocfilehash: bfce85d1690daea2e432496d3fc46662f444a63b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793165"
---
# <a name="c28152"></a>C28152


警告 C28152：与 AddDevice 类似的函数的返回意外执行了 \_ 设备 \_ 初始化

驱动程序已从其 **AddDevice** 例程或类似的实用工具例程中返回，但不会清除 **DeviceObject** 例程中的 "执行 **标记** 字 () **DeviceObject &gt;** " 字样的 **\_ 设备 \_ 初始化** 位。

**AddDevice** 例程必须包含类似于下面的代码，以清除 "**执行 \_ 设备 \_ 初始化**" 标志。

```
FunctionalDeviceObject->Flags &= ~DO_DEVICE_INITIALIZING;
```

有关 **AddDevice** 例程的详细信息，请参阅 [函数或筛选器驱动程序中的 AddDevice 例程](../kernel/adddevice-routines-in-function-or-filter-drivers.md)

 

