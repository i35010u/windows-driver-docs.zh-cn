---
title: 如何实现更改每个跟踪行的前缀输出
description: 如何实现更改每个跟踪行的前缀输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3641a7c51d8d8883307d411b98526a07f3af6b54
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831541"
---
# <a name="how-do-i-change-the-prefix-output-on-every-trace-line"></a>如何更改每个跟踪行中的前缀输出？


使用以下命令更改每个跟踪行的前缀输出：

```
set TRACE_FORMAT_PREFIX=[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!] 
tracefmt -f mytracefile 
```

有关跟踪 \_ 格式 \_ 前缀参数的信息，请参阅 [跟踪消息前缀](trace-message-prefix.md) 主题。









