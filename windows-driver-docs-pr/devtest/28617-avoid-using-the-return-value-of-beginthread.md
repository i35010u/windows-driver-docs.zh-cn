---
title: C28617
description: 警告 C28617 避免使用 _beginthread （） 返回的值。 而是使用 _beginthreadex （）。
ms.assetid: b0de0809-1583-4c1d-ad70-c3e27afc3e6d
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28617
ms.openlocfilehash: c47ab4d9199c1f1def1d76a4172c91dca9d0bc14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545278"
---
# <a name="c28617"></a>C28617


警告 C28617:避免使用返回值的\_beginthread()。 使用\_beginthreadex() 改为

使用更安全 **\_beginthreadex**比 **\_beginthread**。 如果线程生成的 **\_beginthread**很快退出，返回给调用方的句柄 **\_beginthread**可能是无效，或可在更糟的是，指向另一个线程。 但是，通过返回的句柄 **\_beginthreadex**的调用方必须关闭 **\_beginthreadex**，因此它保证是有效的句柄，如果 **\_beginthreadex**未返回错误。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的代码示例将生成此警告。

```
hThread = (HANDLE)_beginthread (&SecondThreadFunc, 0, &args);
WaitForSingleObject (hThread, INFINITE);
```

下面的代码示例可避免此警告。

```
hThread = (HANDLE)_beginthreadex ( NULL, 0,
                                   &SecondThreadFunc,
                                   &args, 0, &threadID);
WaitForSingleObject (hThread, INFINITE);
CloseHandle(hThread);
```

 

 





