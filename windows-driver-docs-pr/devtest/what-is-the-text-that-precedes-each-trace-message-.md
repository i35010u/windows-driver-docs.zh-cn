---
title: 什么是前每条跟踪消息的文本
description: 什么是前每条跟踪消息的文本
ms.assetid: bff8eb0b-f571-405f-b930-3003e2c50621
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aeffbafc960ad92289d51f5ae7738d4582851d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379131"
---
# <a name="what-is-the-text-that-precedes-each-trace-message"></a>每条跟踪消息前面的的文本是什么？


[Tracefmt](tracefmt.md)并[TraceView](traceview.md)添加[跟踪消息前缀](trace-message-prefix.md)到它们格式化每条跟踪消息。 前缀是组成的跟踪消息有关的数据字符串。 Tracefmt 和 TraceView 输出中，可以查看该前缀。

以下行显示跟踪消息前缀的默认语法：

```
[CPUNumber]ProcessID.ThreadID :: SystemTime [MessageGUIDFriendlyName]
```

其中的默认值*MessageGUIDFriendlyName*是在其中的目录[跟踪提供程序](trace-provider.md)生成。

显示的前缀，使用值替换变量后下, 一行中从示例跟踪日志：

```
[0]0C40.0C3C::09/20/2004-14:41:31.625 [tracedrv]Hello, 1 Hi
```

可以添加和删除数据元素由前缀创建或编辑 %跟踪\_格式\_前缀 %环境变量。

有关说明和一组可以包含 %跟踪的值中的数据元素\_格式\_前缀 %，请参阅[跟踪消息前缀](trace-message-prefix.md)。
