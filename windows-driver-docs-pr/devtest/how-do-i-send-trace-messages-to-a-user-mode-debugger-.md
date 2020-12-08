---
title: 如何实现将跟踪消息发送到用户模式调试器
description: 如何实现将跟踪消息发送到用户模式调试器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b2aeeefa73e28ae7041365f2455fa66d1da166
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799761"
---
# <a name="how-do-i-send-trace-messages-to-a-user-mode-debugger"></a>如何将跟踪消息发送到用户模式调试器？


若要将跟踪消息重定向到用户模式调试器，请将 WPP \_ 调试宏添加到源代码中。 将宏的定义指令放在 WPP \_ 控件 \_ guid 定义之后。

WPP \_ 调试宏添加创建跟踪消息的代码，并将消息重定向到宏中指定的目标。 可以将 **DbgPrint** 或 helper 例程与此宏一起使用。

语句的格式如下所示：

```
#define WPP_DEBUG(args) printf args , printf("\n");
```

你可以使用 **DbgPrint** 或 **KdPrint** ，而不是 **printf**，例如：

```
#define WPP_DEBUG(a)   printf a   printf("/n");
```

或

```
#define WPP_DEBUG(b)   DbgPrint("PCI"), DbgPrint b,   DbgPrint("\n");
```

调用例程的语句的格式如下所示：

```
WPP_DEBUG((format, ...))
```

您可以将大多数格式和参数与 WPP \_ 调试配合使用。 但是，不能使用特定于跟踪的格式规范，例如%！IPADDR%.

 

 





