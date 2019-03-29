---
title: C28601
description: 警告 C28601 避免在 HWND_BROADCAST 上发生阻塞。
ms.assetid: 51fc27da-012a-4cf3-adbf-bd7f7c497b01
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28601
ms.openlocfilehash: 4d315286d239433a5e6a33e242fa315a819a3418
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568935"
---
# <a name="c28601"></a>C28601


警告 C28601:避免阻塞 HWND\_广播

此警告指示应用程序调用**SendMessage**与**HWND\_广播**标志，这阻止线程，直到到此消息是广播的响应的所有窗口. 不过，如果没有未响应的另一个窗口，将还会阻止当前线程。

若要解决此问题，请使用**PostMessage**相反，因此它不是阻止调用。 或者，避免使用**HWND\_广播**将定向到特定的窗口消息。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

以下调用可能会导致进程停止响应。

```
SendMessage(HWND_BROADCAST, ... );
```

 

 





