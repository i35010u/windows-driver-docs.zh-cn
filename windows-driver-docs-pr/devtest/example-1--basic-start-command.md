---
title: 示例1基本启动命令
description: 示例1基本启动命令
keywords:
- 跟踪会话 WDK，开始
- 开始命令
- -start 命令
- 启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f41315076eac8ad2c8a3e6d8b62c7bf16c89ec58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787653"
---
# <a name="example-1-basic-start-command"></a>示例 1：基本启动命令


以下命令是启动标准跟踪会话的最简单命令的示例：

```
tracelog -start MyTrace
```

此命令启动名为 "MyTrace" 的会话。 此会话具有其他会话属性的默认值，其中包括默认位置 C LogFile 中的日志文件 \\ 。

如果此命令不包括会话名称，Tracelog 将启动 NT 内核记录器跟踪会话，这是默认设置。

因为该命令不包含 **-guid** 参数，所以没有为跟踪会话启用任何提供程序，但你可以使用 **tracelog** 命令在此会话启动后将提供程序添加到此会话。 有关如何使用 **-enable** 命令的示例，请参阅 [示例5：启用跟踪提供程序](example-5--enabling-trace-providers.md)。
