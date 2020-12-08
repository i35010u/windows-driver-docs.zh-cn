---
title: 如何实现调试跟踪失败
description: 如何实现调试跟踪失败
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 453e8c48ced74daf4286fe2963631a3483945df1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795085"
---
# <a name="how-do-i-debug-tracing-failures"></a>如何调试跟踪错误？


若要调试跟踪检测驱动程序的问题（例如跟踪日志文件中未显示的跟踪消息，即使启用了提供程序），请将 **WppDebug** 宏定义添加到源代码中。

**WppDebug** 启用旨在调试 WPP 的代码。 它会跟踪注册和启用/禁用活动等操作。

任何 **WppDebug** 定义指令都将起作用。 例如：

```
#define WppDebug(a,b) printf b, printf("\n");
```

若要调用例程，请使用以下格式：

```
WppDebug(level,(format,...));
```

不要将跟踪 WPP 操作的 **WppDebug** 宏与将跟踪消息发送到调试器的 **wpp \_ 调试** 宏混淆。

 

 





