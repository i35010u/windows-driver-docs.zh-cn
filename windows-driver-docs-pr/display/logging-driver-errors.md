---
title: 记录驱动程序错误
description: 记录驱动程序错误
ms.assetid: 7deb2a9a-70aa-4660-a0c8-e118e03eef3b
keywords:
- 错误日志 WDK 显示
- 错误 WDK 显示
- 记录 WDK 显示的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28cea0f52cff495f1f2a7fcc1fc0f849a9ce087
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347540"
---
# <a name="logging-driver-errors"></a>记录驱动程序错误


Microsoft DirectX 图形内核子系统 (*Dxgkrnl.sys*) 记录向内存中的日志显示驱动程序相关的错误、 断言、 警告和事件 (在*Watchdog.sys*)。

除了将信息记录到日志中，默认情况下，检查生成版本的 DirectX 图形内核子系统强行进入的附加调试器如果出现错误或断言。 通过默认情况下，DirectX 图形内核子系统只记录错误和日志的断言的免费内部版本号和如果出现错误或断言不会中断到调试器。 可以通过首先创建以下注册表更改此默认行为\_注册表中的 DWORD 项：

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Logging\BreakOnAssertion
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Logging\BreakOnError
```

若要使调试器启动如果出现错误或断言，应设置的值**BreakOnError**或**BreakOnAssertion**为 1 (TRUE) 分别。 若要使如果出现错误或断言不会启动调试器，应设置的值**BreakOnError**或**BreakOnAssertion**为 0 (FALSE) 分别。

 

 





