---
title: 示例5启用跟踪提供程序
description: 示例5启用跟踪提供程序
keywords:
- Tracelog WDK，提供程序
- 提供程序 WDK 软件跟踪
- 跟踪 WDK，提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8bbe98750b709ac7c63e039b916f053acd28060
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784037"
---
# <a name="example-5-enabling-trace-providers"></a>示例 5：启用跟踪提供程序

以下命令将对名为 "MyTrace" 的正在运行的跟踪会话启用跟踪提供程序：

```
tracelog -enable MyTrace -guid MyProvider.guid
```

作为响应，Tracelog 将启用由 MyProvider 文件中的 Guid 表示的提供程序。 此命令不会更改跟踪会话的任何其他属性。

您可以启动跟踪会话，然后启用提供程序，也可以在启动跟踪会话时启用提供程序。 例如，以下命令将启动跟踪会话，然后启用提供程序：

```
tracelog -start MyTrace
tracelog -enable MyTrace -guid MyProvider.guid
```

与此相反，以下命令将启动会话并在一个命令中启用提供程序：

```
tracelog -start MyTrace -guid MyProvider.guid
```

除了计时差异外，这些命令的效果是相同的。

通常， **tracelog** 命令用于更改与提供程序关联的标志和级别。 由于标志和级别是提供程序的属性，而不是跟踪会话的属性，因此可以使用 **tracelog** 命令而不是 **tracelog** 命令来更改它们。

以下命令在 MyProvider 文件中更改提供程序的标志和级别。 必须使用 **-guid** 参数指定跟踪提供程序，即使该提供程序是为跟踪会话启用的唯一访问接口。

```
tracelog -enable MyTrace -guid MyProvider.guid -flag 2 -level 2
```

还可以使用 **tracelog** 命令向跟踪会话添加更多提供程序，并使用 **tracelog** 命令重新启用已禁用的提供程序。
