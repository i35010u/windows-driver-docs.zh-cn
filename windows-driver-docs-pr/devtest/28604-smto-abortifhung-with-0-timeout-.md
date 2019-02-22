---
title: C28604
description: 警告 C28604 避免使用 SMTO_ABORTIFHUNG 调用 SendMessageTimeout 超时值为 0。
ms.assetid: d9be9747-20f6-4a2b-a841-eaf3255f2f65
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28604
ms.openlocfilehash: 15a702c26f1f54b9ee7d8cff14e93136095f2c53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543743"
---
# <a name="c28604"></a>C28604


警告 C28604:避免使用 SMTO 调用 SendMessageTimeout\_ABORTIFHUNG 具有为 0 的超时值

代码分析工具将报告此警告，如果应用程序调用**SendMessageTimeout**与**SMTO\_ABORTIFHUNG**标志和超时期限为零。 使用**SendMessageTimeout**因为超时期限不起作用，并在调用被视为是阻塞调用，这种方式可能会产生问题。

指定超时期限的非零值。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

以下函数调用可能会导致无限期地响应过程。

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

以下函数调用不存在此问题。

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

 

 





