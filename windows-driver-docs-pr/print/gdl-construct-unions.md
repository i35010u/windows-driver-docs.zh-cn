---
title: GDL 构造联合
description: GDL 构造联合
keywords:
- 构造 WDK GDL，联合
- 逻辑构造 WDK GDL
- 构造 WDK GDL，逻辑构造
- 构造 WDK GDL，示例
- 同级构造 WDK GDL
- 联合 WDK GDL
- 分析器 WDK GDL，处理联合
- GDL WDK，联合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 088981367776a5606cf87048294add754d07bb6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835993"
---
# <a name="gdl-construct-unions"></a>GDL 构造联合


如果在 GDL 源文件中定义了多个具有相同构造类型和构造标记的构造，该构造 ([逻辑构造](syntactical-and-logical-constructs-in-gdl.md)) 的逻辑表示形式将包含 GDL 源文件中定义的原始构造的内容的并集。

构造类型和构造标记一起在其父) 的上下文中唯一指定或定义逻辑构造 (。 与 XML 不同，定义了两个 *同级* 构造后，每个构造具有相同的构造类型和构造标记，结果为一个逻辑构造。 事实上，构造甚至不需要为非同级语法，它们也可以是逻辑同级。  (*语法同级* 显式驻留在同一构造主体中，而 *逻辑同级* 都是同一逻辑构造的子。 ) 

逻辑构造的内容是同级内容的联合。 快照中显示的内容是逻辑构造，而不是在 GDL 源文件中最初进行语法定义的构造。 在下面的代码示例中，有两个同级构造，两者都是构造类型： \* Person 和 With 构造标记： FlorenceF。

```cpp
*Person: FlorenceF
{
*Name: Florence Flipo
*Company:Contoso Pharmaceuticals
{
*Location: Redmond, WA
}
}
*Person: FlorenceF
{
*Position: CEO
*Company:Contoso Pharmaceuticals
{
*NumberOfEmployees: 43,000
}
}
```

根据上述规则，两个同级定义一个逻辑构造，其中包含两个同级的联合。

```cpp
*Person: FlorenceF
{
*Name: Florence Flipo
*Company:Contoso Pharmaceuticals
{
*Location: Redmond, WA
}
*Position: CEO
*Company:Contoso Pharmaceuticals
{
*NumberOfEmployees: 43,000
}
}
```

请注意，上一示例中的合并已创建两个具有相同构造类型的新同级构造： \* Contoso 制药。

如果 (递归) 再次应用相同的规则，则会生成以下代码。

```cpp
*Person: FlorenceF
{
*Name: Florence Flipo
*Company:Contoso Pharmaceuticals
{
*Location: Redmond, WA
*NumberOfEmployees: 43,000
}
*Position: CEO
}
```

在分析上述三个 GDL 片段时，会生成相同的内部表示形式。 内部表示形式最接近于最后一个片段。

如果对具有相同[关键字](gdl-keywords.md)的[属性](gdl-attributes.md)进行了多次定义，则不会发生任何合并。 每个定义仍存在于内部表示形式中。 模板指令 **\* 累加** 性用于指定将哪些值或值传输到快照。

GDL 分析器采用 GDL 流的语法表示形式，并创建 GDL 命令的内部逻辑表示形式。 然后，这些命令的内部表示形式将转换为 XML，并成为快照。

 

 




