---
title: GDL 构造分隔符
description: GDL 构造分隔符
ms.assetid: 6f759534-3dc2-4e04-afe0-3f377790be21
keywords:
- 构造 WDK GDL，分隔符
- GDL WDK 构造
- 分析器 WDK GDL，处理构造分隔符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93560efa1e0ba3ac3c92f4ce533d9545ac230f48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566179"
---
# <a name="gdl-construct-delimiters"></a>GDL 构造分隔符


*构造分隔符*字符是大括号: {和}。 构造的分隔符字符此外的行为类似于换行符，因此你必须按照或位于与 linebreak 序列构造分隔符。

以下两个代码示例演示构造分隔符使用。 第一个示例具有分散在多个行的值。

```cpp
*Person: FlorenceF
{
 *Company:Contoso Pharmaceuticals
 {
 *Location: Redmond, WA
 }
}
```

第二个示例将值合并为一行，但仍使用大括号来分隔各值的部分。

```cpp
*Person: FlorenceF{*Company:Contoso Pharmaceuticals{*Location: Redmond, WA}}
```

 

 




