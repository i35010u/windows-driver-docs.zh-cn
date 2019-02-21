---
title: 如何将跟踪消息发送给用户模式下调试程序
description: 如何将跟踪消息发送给用户模式下调试程序
ms.assetid: d1a9df10-3339-4518-a42a-abd1123d5e21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2085f7643b12c3315855bcfa481c814b6164f38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524322"
---
# <a name="how-do-i-send-trace-messages-to-a-user-mode-debugger"></a>如何将跟踪消息发送给用户模式下调试程序？


若要将跟踪消息重定向到用户模式下调试程序，将添加 WPP\_源代码调试宏。 将宏的定义指令放在后面 WPP\_控制\_GUID 定义。

WPP\_调试宏将添加代码，创建的跟踪消息，并将该消息重定向到在宏中指定的目标。 可以使用**DbgPrint**或使用该宏的帮助器例程。

语句的格式如下所示：

```
#define WPP_DEBUG(args) printf args , printf("\n");
```

可以使用**DbgPrint**或**KdPrint**而不是**printf**，例如：

```
#define WPP_DEBUG(a)   printf a   printf("/n");
```

或者

```
#define WPP_DEBUG(b)   DbgPrint("PCI"), DbgPrint b,   DbgPrint("\n");
```

调用例程的语句的格式如下所示：

```
WPP_DEBUG((format, ...))
```

您可以将大多数格式和自变量与 WPP\_调试。 但是，不能使用的特定于跟踪的格式规范，例如 %！IPADDR %。

 

 





