---
title: 示例4序列号
description: 示例4序列号
keywords:
- Tracefmt WDK，序列号
- 序列号 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06f4da063231e856cd5ffb9fc4ddb8a2297517d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839139"
---
# <a name="example-4-sequence-numbers"></a>示例 4：序列号


以下命令在输出文件中包括消息的本地序列号或全局序列号。 如果未生成序列号，则序列字段包含零。

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.txt -seq
```

此命令通过使用 c：跟踪目录中的 TMF 文件来格式化 mytrace 日志文件中的消息 \\ 。 它将格式化消息写入 mytrace.txt 文件中。 该命令使用 **-seq** 参数来指示 Tracefmt 在输出文件中包含序列号。

输出文件的摘选如下所示：

```text
[0]0AF4.0C64::07/25/2003-13:55:39.998 00004ea4 [tracedrv]IOCTL = 1
[0]0AF4.0C64::07/25/2003-13:55:39.998 000047d0 [tracedrv]Hello, 1 Hi
[0]0AF4.0C64::07/25/2003-13:55:39.998 63966c89 [tracedrv]Hello, 2 Hi
...
```
