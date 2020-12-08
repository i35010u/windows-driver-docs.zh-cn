---
title: 每个跟踪消息前面的文本是什么
description: 每个跟踪消息前面的文本是什么
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1304275ddc7779dd0d86fe06eaa6200842f2fa08
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810697"
---
# <a name="what-is-the-text-that-precedes-each-trace-message"></a>每条跟踪消息前面的的文本是什么？


[Tracefmt](tracefmt.md) 和 [TraceView](traceview.md) 为其格式的每个跟踪消息添加一个 [跟踪消息前缀](trace-message-prefix.md) 。 前缀是由有关跟踪消息的数据组成的字符串。 可以在 Tracefmt 和 TraceView 输出中查看前缀。

以下行显示了跟踪消息前缀的默认语法：

```
[CPUNumber]ProcessID.ThreadID :: SystemTime [MessageGUIDFriendlyName]
```

其中， *MessageGUIDFriendlyName* 的默认值是在其中生成 [跟踪提供程序](trace-provider.md) 的目录。

带有替换变量的值的前缀在示例跟踪日志中显示为以下行：

```
[0]0C40.0C3C::09/20/2004-14:41:31.625 [tracedrv]Hello, 1 Hi
```

可以通过创建或编辑% TRACE \_ FORMAT \_ prefix% 环境变量来添加和删除前缀中的数据元素。

有关说明和可包含在% 跟踪格式前缀% 的值中的数据元素列表 \_ \_ ，请参阅 [跟踪消息前缀](trace-message-prefix.md)。
