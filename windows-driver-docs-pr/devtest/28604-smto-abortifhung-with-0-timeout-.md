---
title: C28604
description: 警告 C28604 避免使用超时值为0的 SMTO_ABORTIFHUNG 调用 SendMessageTimeout。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28604
ms.openlocfilehash: 5bf6711c0076f344e0500a1746c3d5ced74539e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823401"
---
# <a name="c28604"></a>C28604


警告 C28604：避免使用 SMTO ABORTIFHUNG 调用 SendMessageTimeout， \_ 超时值为0

当应用程序调用带有 **SMTO \_ ABORTIFHUNG** 标志的 **SendMessageTimeout** 和超时期限为零时，代码分析工具将报告此警告。 以这种方式使用 **SendMessageTimeout** 可能会出现问题，因为超时期限不起作用，并且调用被视为阻止调用。

指定超时期限的非零值。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

以下函数调用可能会导致该进程不会无限期地做出响应。

```
fNeedsCallbackEvent = (0 != SendMessageTimeout(
_hwnd, 
WM_NULL, 
0,
0, 
SMTO_ABORTIFHUNG,
0,
&dwResult)); 
```

以下函数调用没有此问题。

```
fNeedsCallbackEvent = (0 != SendMessageTimeout(
_hwnd, 
WM_NULL, 
0,
0,
SMTO_ABORTIFHUNG,
1000,  
&dwResult)); 
```

 

 





