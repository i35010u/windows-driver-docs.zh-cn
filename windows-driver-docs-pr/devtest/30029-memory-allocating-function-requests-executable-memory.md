---
title: C30029
description: 警告 C30029 调用请求可执行内存的内存分配函数。
ms.date: 12/10/2020
ms.localizationpriority: medium
f1_keywords:
- C30029
ms.openlocfilehash: 7973f6b887e38e96906a644f2cc74d479531b9dc
ms.sourcegitcommit: 6395b4691c2c5f01995dcec00bcf2eb1f31acd55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97103648"
---
# <a name="c30029"></a>C30029


警告 C30029：调用请求可执行内存的内存分配函数

禁止的 \_ 内存 \_ 分配 \_ NOTYPE

某些 Api 仅分配可执行的非分页池。 没有可提供的参数将更改此行为。 解决此问题的唯一方法是使用备用 API，该 API 允许分配不可执行的非分页池内存。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


下面的代码生成警告 C30029：

```
MmMapIoSpace(  PhysicalAddress,
        numberOfBytes,
        MmNonCached);
```

下面的代码可避免此警告：

```
MmMapIoSpaceEx(    PhysicalAddress,
        numberOfBytes,
        PAGE_NOCACHE | PAGE_READWRITE);
```

 

 





