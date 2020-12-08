---
title: C28617
description: '警告 C28617 避免使用 ( # A1 _beginthread 的返回值。 改为使用 _beginthreadex ( # A1。'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28617
ms.openlocfilehash: ec4776b10012277a2edca83888c74519e66bdfad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795637"
---
# <a name="c28617"></a>C28617


警告 C28617：避免使用 \_ beginthread ( # A1 的返回值。 改为使用 \_ beginthreadex ( # A1

使用 **\_ beginthreadex** 比 **\_ beginthread** 更安全。 如果由 **\_ beginthread** 生成的线程很快退出，则返回给 **\_ beginthread** 的调用方的句柄可能无效，或者更糟的是指向另一个线程。 但是，由 **\_ beginthreadex** 返回的句柄必须由 **\_ beginthreadex** 的调用方关闭，因此如果 **\_ beginthreadex** 未返回错误，则可以保证其为有效句柄。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的代码示例将生成此警告。

```
hThread = (HANDLE)_beginthread (&SecondThreadFunc, 0, &args);
WaitForSingleObject (hThread, INFINITE);
```

下面的代码示例可避免出现此警告。

```
hThread = (HANDLE)_beginthreadex ( NULL, 0,
                                   &SecondThreadFunc,
                                   &args, 0, &threadID);
WaitForSingleObject (hThread, INFINITE);
CloseHandle(hThread);
```

 

 





