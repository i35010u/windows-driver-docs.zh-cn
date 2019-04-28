---
title: C30029
description: 警告 C30029 调用的分配函数的内存请求可执行文件的内存。
ms.assetid: E32E6EDB-010A-4E7F-8505-1E7557BB3FDF
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30029
ms.openlocfilehash: 0b1b9772cffc84738135cc75701ddab148492b26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347055"
---
# <a name="c30029"></a>C30029


警告 C30029:调用的内存分配请求可执行文件的内存的函数

已禁止\_内存优化\_分配\_NOTYPE

某些 Api 仅可执行文件的非分页缓冲的池分配。 不没有可以提供任何参数，它将改变此行为。 若要解决此问题的唯一方法是使用一种替代方法进行的非可执行文件的非分页缓冲的池内存分配的 API。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的代码生成警告 C30029:

```
MmMapIoSpace(  PhysicalAddress,
        numberOfBytes,
        PAGE_NOCACHE);
```

下面的代码可避免此警告：

```
MmMapIoSpaceEx(    PhysicalAddress,
        numberOfBytes,
        PAGE_NOCACHE | PAGE_READWRITE);
```

 

 





