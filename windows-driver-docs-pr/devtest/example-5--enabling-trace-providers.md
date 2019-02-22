---
title: 示例 5 启用跟踪提供程序
description: 示例 5 启用跟踪提供程序
ms.assetid: 405aea85-0248-4fd3-82eb-1beb76cc8a1b
keywords:
- Tracelog WDK，提供程序
- 提供程序 WDK 软件跟踪
- 跟踪 WDK，提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 275e45d68b20694325270788883132626a941f42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540885"
---
# <a name="example-5-enabling-trace-providers"></a>示例 5:启用跟踪提供程序

以下命令启用名为"MyTrace"运行跟踪会话的跟踪提供程序：

```
tracelog -enable MyTrace -guid MyProvider.guid
```

在响应中，跟踪日志启用 MyProvider.guid 文件中的 Guid 所表示的提供程序。 该命令不会更改跟踪会话的任何其他属性。

你可以启动跟踪会话，然后启用提供程序，或启动跟踪会话时，可以启用的提供程序。 例如，以下命令启动跟踪会话，然后启用提供程序：

```
tracelog -start MyTrace
tracelog -enable MyTrace -guid MyProvider.guid
```

与此相反，以下命令启动会话并启用在一个命令中的提供程序：

```
tracelog -start MyTrace -guid MyProvider.guid
```

非计时的差异，这些命令的效果是相同的。

通常情况下， **tracelog-启用**命令用于更改标志和与提供程序关联的级别。 由于标志和级别是属性的提供程序不是属性的跟踪会话，因此使用**tracelog-启用**未命令**tracelog-更新**命令中，若要更改它们。

以下命令将更改 MyProvider.guid 文件中的提供程序的标志和级别。 必须使用**guid**参数来指定跟踪提供程序，即使该提供程序是唯一的提供程序启用跟踪会话。

```
tracelog -enable MyTrace -guid MyProvider.guid -flag 2 -level 2
```

此外可以使用**tracelog-启用**命令将更多提供程序添加到跟踪会话，并重新启用已禁用使用的提供程序**tracelog-禁用**命令。
