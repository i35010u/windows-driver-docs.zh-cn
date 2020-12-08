---
title: C28129
description: 警告 C28129 已对操作数进行了赋值，只应使用位集修改并清除。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28129
ms.openlocfilehash: 279c8a23742540e6c9cbe316ec62e2af91ff58cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830735"
---
# <a name="c28129"></a>C28129


警告 C28129：已对操作数进行了赋值，只应使用位集进行修改并清除

驱动程序使用赋值来修改操作数。 分配值时，可能会无意中更改需要更改的其他位的值，导致意外后果。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
fdo->Flags = DO_BUFFERED_IO;
```

下面的代码示例可避免此警告。

```
fdo->Flags |= DO_BUFFERED_IO;
```

 

 





