---
title: 示例 1 基本 Start 命令
description: 示例 1 基本 Start 命令
ms.assetid: be5abbf0-727d-430b-a427-66cc61f3445c
keywords:
- 跟踪会话 WDK，启动
- 启动命令
- -启动命令
- 启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65accf8e96bf70ccdd318b93e817e676db4d6e4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534391"
---
# <a name="example-1-basic-start-command"></a>示例 1：基本启动命令


下面的命令是启动一个标准跟踪会话的最简单命令示例：

```
tracelog -start MyTrace
```

此命令启动名为"MyTrace"的会话。 会话具有其他会话属性，在默认位置中，C 包括日志文件的默认值\\LogFile.etl。

如果该命令未包括会话名称，跟踪日志将启动 NT 内核记录器跟踪会话，这是默认值。

因为该命令不包括**guid**参数，任何提供程序启用跟踪会话，但可以使用**tracelog-启用**命令，将提供程序添加到此会话启动后。 请参阅[示例 5:启用跟踪提供程序](example-5--enabling-trace-providers.md)有关如何使用的示例 **-启用**命令。
