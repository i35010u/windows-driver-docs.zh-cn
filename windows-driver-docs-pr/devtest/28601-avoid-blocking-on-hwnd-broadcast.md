---
title: C28601
description: 警告 C28601 避免 HWND_BROADCAST 上出现阻止。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28601
ms.openlocfilehash: 1a6f38d44582c88d262a602a9d403ae289e0ae7d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799789"
---
# <a name="c28601"></a>C28601


警告 C28601：避免在 HWND 广播上阻止 \_

此警告表明，应用程序调用了包含 **HWND \_ 广播** 标志的 **SendMessage** ，这会阻止线程，直到此消息广播到的所有窗口响应。 但是，如果存在其他不响应的窗口，则当前线程也将被阻止。

若要解决此问题，请改用 **PostMessage** ，使其不是阻止调用。 或者，避免使用 **HWND \_ 广播** 将消息定向到特定窗口。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

以下调用可能会导致进程停止响应。

```
SendMessage(HWND_BROADCAST, ... );
```

 

 





