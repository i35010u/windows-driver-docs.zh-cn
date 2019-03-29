---
title: GDL 构造联合
description: GDL 构造联合
ms.assetid: 0ca237fe-7f47-4b9c-8963-676a2afd1140
keywords:
- 构造 WDK GDL，联合
- 逻辑构造 WDK GDL
- 构造 WDK GDL，逻辑构造
- 构造 WDK GDL，示例
- 同级构造 WDK GDL
- 联合 WDK GDL
- 分析器 WDK GDL，处理联合
- GDL WDK 联合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d657e3fbb9bc98a70d394d2bd25b0cc55a89bd5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562778"
---
# <a name="gdl-construct-unions"></a>GDL 构造联合


如果具有相同的多个构造构造类型和 GDL 源中定义构造标记文件，该构造的逻辑表示形式 ([逻辑构造，](syntactical-and-logical-constructs-in-gdl.md)) 将包含的原始内容的并集GDL 源代码文件中定义的构造。

构造类型和构造标记一起唯一地指定或定义一种逻辑构造 （在其父项的上下文）。 与 XML，当两个不同*同级*定义了构造，每个都具有相同的构造类型和构造标记，则结果是一个逻辑构造。 事实上，甚至是语法同级不需要构造，它们可以是逻辑的同级。 (*语法同级*显式驻留在同一构造正文中，并*逻辑同级*这两个子级的同一个逻辑构造。)

逻辑构造的内容是同级元素的内容的联合。 在快照中显示的内容是逻辑构造，未构造，因为它们最初语法定义 GDL 源文件中。 在下面的代码示例中，有两个同级构造，它们都具有构造类型：\*人员和具有构造标记：FlorenceF。

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

根据上述规则，两个同级定义单一的逻辑构造，它包含两个同级的并集。

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

请注意，在前面的示例合并已创建具有相同的构造类型的两个新的同级构造：\*公司和构造标记：Contoso Pharmaceuticals。

如果应用相同规则再次 （以递归方式），下面的代码会产生。

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

任何时对其进行分析，上述三个 GDL 片段生成相同的内部表示形式。 内部表示形式最近似的最后一个片段。

当[特性](gdl-attributes.md)具有相同[关键字](gdl-keywords.md)multiply 是定义，没有合并会发生。 每个定义仍存在于内部表示形式。 模板指令**\*累加性**用来指定哪些值传输到快照。

GDL 分析器采用 GDL 流的语法表示形式，并创建内部 GDL 命令的逻辑表示形式。 这些命令的内部表示形式然后转换为 XML，并将变为快照。

 

 




