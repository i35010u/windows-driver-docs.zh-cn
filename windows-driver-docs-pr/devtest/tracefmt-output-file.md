---
title: Tracefmt 输出文件
description: Tracefmt 输出文件
keywords:
- Tracefmt WDK，输出文件
- 输出文件 WDK Tracefmt
- 文件 WDK Tracefmt
- out 文件
- out 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fe978bbbe4a6b50a8ac7a1e12305fcf5dcadaf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817413"
---
# <a name="tracefmt-output-file"></a>Tracefmt 输出文件


Tracefmt 输出 ( 输出) 文件是一个文本文件，它以用户可读的格式从跟踪日志或实时跟踪会话中显示跟踪消息。 每个跟踪消息前面都有一个可自定义的 [跟踪消息前缀](trace-message-prefix.md)。

Tracefmt 输出文件是可选的。 可以指示 Tracefmt 显示跟踪消息，但不会创建输出文件，也可以同时显示跟踪消息并将其记录到输出文件中。

Tracefmt 输出文件通常用作分析和筛选跟踪消息的其他程序的输入。

下面是 Tracefmt 输出文件的内容的摘要，其中包含 Tracedrv，这是一个针对软件跟踪进行检测的示例驱动程序。 [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)是设计用于软件跟踪的示例驱动程序，位于 GitHub 上的 [Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples) 存储库中。

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

 

 





