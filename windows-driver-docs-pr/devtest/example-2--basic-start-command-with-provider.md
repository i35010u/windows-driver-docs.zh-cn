---
title: 与提供程序的示例 2 基本 Start 命令
description: 与提供程序的示例 2 基本 Start 命令
ms.assetid: 86730943-107e-441a-a860-4df540bc0426
keywords:
- 跟踪会话 WDK，启动
- 启动命令
- -启动命令
- guid 参数
- -guid 参数
- 启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ad3f3e0687e8e2d494e10d090662d898e290a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344700"
---
# <a name="example-2-basic-start-command-with-provider"></a>示例 2：使用提供程序的基本启动命令

以下启动命令是到示例 1 中的命令相同，但它使用**guid**参数来启用用于跟踪会话提供程序：

```
tracelog -start MyTrace -guid #d58c126f-b309-11d1-969e-0000f875a5bc
```

该命令启动名为"My Trace"的跟踪会话。 它使用**guid**参数来指定控件的跟踪提供程序的 GUID。 GUID 前面加一个数字符号 (**\#**) 以指示它是一个 GUID 而不是 GUID 文件名称。

在响应中，跟踪日志启动 MyTrace 跟踪日志会话并启用由 GUID 指定的提供程序。 它使用默认值的其他属性的会话，包括创建日志文件在 c:\\LogFile.etl。

如果未指定 （在此情况下，"MyTrace"） 的跟踪会话的名称，Tracelog 启动 NT 内核记录器跟踪会话，这是默认值。

如果未指定标志或级别，某些提供程序可能不会生成跟踪消息，即使启用它们。
