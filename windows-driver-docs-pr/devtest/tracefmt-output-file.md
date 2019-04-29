---
title: Tracefmt 输出文件
description: Tracefmt 输出文件
ms.assetid: 55c8964c-992f-468c-83ea-0316fcb12110
keywords:
- Tracefmt WDK 的输出文件
- 输出文件 WDK Tracefmt
- 文件 WDK Tracefmt
- .out 文件
- 出文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98132e51949b9c29b8affce8bc458fb4db42a04d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373107"
---
# <a name="tracefmt-output-file"></a>Tracefmt 输出文件


Tracefmt 输出 (.out) 文件是以用户可读格式显示从跟踪日志或实时跟踪会话的跟踪消息的文本文件。 每条跟踪消息前面通过可自定义[跟踪消息前缀](trace-message-prefix.md)。

Tracefmt 输出文件是可选的。 你可以直接 Tracefmt 显示跟踪消息，但不是能创建输出文件，也可以同时显示跟踪消息和输出文件中记录这些。

Tracefmt 输出文件通常用作其他程序的分析和筛选跟踪消息的输入。

下面是内容的与 Tracedrv，检测软件跟踪的一个示例驱动程序的跟踪会话 Tracefmt 输出文件的一段摘录。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)，为软件跟踪设计的一个示例驱动程序现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

```
EventTrace
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]IOCTL = 1
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 1 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 2 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 3 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 4 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 5 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 6 Hi
```

 

 





