---
title: 示例 4 序列号
description: 示例 4 序列号
ms.assetid: 5b498267-c495-4a25-abb9-aa83a51559e1
keywords:
- Tracefmt WDK、 序列号
- 序列号 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0c141cffa79d9188d7fff476f776d4aecd26052
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521354"
---
# <a name="example-4-sequence-numbers"></a>示例 4:序列号


以下命令在输出文件中包含消息的本地或全局序列的号。 如果没有生成序列号，序列字段将包含零。

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.txt -seq
```

此命令通过使用 c： 驱动器中的 TMF 文件格式 mytrace.etl 日志文件中的消息\\跟踪目录。 它将格式化的消息写入 mytrace.txt 文件中。 该命令使用 **-seq**参数指示 Tracefmt 输出文件中包含序列号。

输出文件的一段摘录显示，如下所示：

```text
[0]0AF4.0C64::07/25/2003-13:55:39.998 00004ea4 [tracedrv]IOCTL = 1
[0]0AF4.0C64::07/25/2003-13:55:39.998 000047d0 [tracedrv]Hello, 1 Hi
[0]0AF4.0C64::07/25/2003-13:55:39.998 63966c89 [tracedrv]Hello, 2 Hi
...
```
