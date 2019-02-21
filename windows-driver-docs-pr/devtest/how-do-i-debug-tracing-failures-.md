---
title: 如何调试跟踪故障
description: 如何调试跟踪故障
ms.assetid: 9f974482-e19d-4bcc-a884-4425741aa465
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cf79c687a7131fbd90790ebff82bff137459d31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521051"
---
# <a name="how-do-i-debug-tracing-failures"></a>如何调试跟踪故障？


若要调试问题的跟踪检测驱动程序，如跟踪消息的未显示在跟踪日志文件中，即使启用了提供程序，添加**WppDebug**对源代码的宏定义。

**WppDebug**使代码旨在调试 WPP。 它跟踪操作，如注册和启用/禁用活动。

任何**WppDebug**定义指令将起作用。 例如：

```
#define WppDebug(a,b) printf b, printf("\n");
```

若要调用该例程，使用以下格式：

```
WppDebug(level,(format,...));
```

不要混淆**WppDebug**宏，与跟踪 WPP 操作**WPP\_调试**宏，将跟踪消息发送到调试程序。

 

 





