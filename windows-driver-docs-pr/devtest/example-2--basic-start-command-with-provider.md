---
title: 示例2具有提供程序的基本启动命令
description: 示例2具有提供程序的基本启动命令
keywords:
- 跟踪会话 WDK，开始
- 开始命令
- -start 命令
- guid 参数
- -guid 参数
- 启动跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df70a259de12f5850bf81395b5c55e25d1c5e8a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839145"
---
# <a name="example-2-basic-start-command-with-provider"></a>示例 2：使用提供程序的基本启动命令

以下 start 命令与示例1中的命令相同，不同之处在于它使用 **-guid** 参数启用跟踪会话的提供程序：

```
tracelog -start MyTrace -guid #d58c126f-b309-11d1-969e-0000f875a5bc
```

命令启动名为 "My Trace" 的跟踪会话。 它使用 **-guid** 参数指定跟踪提供程序的控件 guid。 GUID 前面有一个数字符号 (**\#**) ，指示它是一个 guid，而不是 guid 文件名。

作为响应，Tracelog 将启动 MyTrace 跟踪日志会话，并启用 GUID 指定的提供程序。 它使用会话的其他属性的默认值，包括在 C： LogFile 中创建日志文件 \\ 。

如果未指定跟踪会话的名称 (在此示例中为 "MyTrace" ) ，则 Tracelog 将启动 NT 内核记录器跟踪会话（这是默认值）。

如果未指定标志或级别，则某些提供程序可能不会生成跟踪消息（即使它们已启用）。
