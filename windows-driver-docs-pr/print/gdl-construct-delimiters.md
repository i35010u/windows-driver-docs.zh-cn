---
title: GDL 构造分隔符
description: GDL 构造分隔符
keywords:
- 构造 WDK GDL，分隔符
- GDL WDK、构造
- 分析器 WDK GDL，处理构造分隔符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7e059136a3082f2fe5d44bab4b9d3dbd2d224ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797031"
---
# <a name="gdl-construct-delimiters"></a>GDL 构造分隔符


*构造分隔符* 字符为大括号： {和}。 构造分隔符字符还具有类似于换行符的行为，因此，必须在构造分隔符前面使用 linebreak 序列。

下面两个代码示例演示了构造分隔符的用法。 第一个示例将值分散到多个行。

```cpp
*Person: FlorenceF
{
 *Company:Contoso Pharmaceuticals
 {
 *Location: Redmond, WA
 }
}
```

第二个示例将该值合并为一行，但仍使用大括号来分隔值的各个部分。

```cpp
*Person: FlorenceF{*Company:Contoso Pharmaceuticals{*Location: Redmond, WA}}
```

 

 




