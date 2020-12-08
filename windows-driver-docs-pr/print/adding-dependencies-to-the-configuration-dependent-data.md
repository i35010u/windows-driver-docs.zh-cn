---
title: 将依赖项添加到配置相关的数据
description: 将依赖项添加到配置相关的数据
keywords:
- GDL WDK，配置
- 配置 WDK GDL，添加依赖项
- 将依赖项添加到与配置相关的数据 WDK GDL
- 依赖于配置的数据 WDK GDL 中的依赖关系
- Switch/Case 指令 WDK GDL
- 功能/选项指令 WDK GDL
- 构造 WDK GDL，default 构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0df96ca04ebaba841b1cd3c80d6af43e95329422
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812425"
---
# <a name="adding-dependencies-to-the-configuration-dependent-data"></a>将依赖项添加到配置相关的数据


**\* Switch** / **\* Case** 指令使数据依赖于使用 **\* 功能** / **\* 选项** 指令定义的参数。 **\* Switch** 构造的构造标记将命名 **\* 功能** 构造中定义的一个参数。 **\* 开关** 构造的构造标记对参数的引用可能在其定义之前通过 **\* 功能** 构造。

**\* Switch** 构造的主体包含若干个 **\* Case** 构造和一个可选的 **\* 默认** 构造。 **\* Switch** 构造内不能出现其他子条目。 **\* Case** 构造的构造标记会将在 **\* 选项** 构造中定义的一个允许值命名为对应于 **\* Switch** 构造中命名的参数。 构造标记不用于<strong> \* 默认</strong>构造。

**\* Switch** 构造可以作为任何其他构造中的子条目出现，只不过 **\* switch** 构造不能是另一个 **\* switch** 构造的子级。 **\* Case** 构造的主体可以包含任何 GDL 项，只不过 **\* 事例** 构造不能是 **\* 功能** 或 **\* 默认** 构造的上级。

**\* Switch** / **\* Case** 指令的工作方式非常类似于具有相同名称的 C 语言构造。 在配置中将构造标记命名为的任何 **\* Case** 构造 (的内容将被指定为 **\* Switch** 构造) 的参数的当前值或状态，并允许它们显示在快照中。 否则，分析器会阻止 **\* 事例** 构造中包含的条目出现在快照中。

**注意**  与 C 版本的 **\* Switch** / **\* Case** 不同，GDL 不需要 break 语句来停止执行，而不需要在事例构造结束 **\* 时** 继续执行。

 

如果省略 <strong> \* case</strong>构造的主体 (即， **\* case** 显示为属性而不是构造) ，则将使用下一 **\* 种 case** 或 **\* 默认** 构造的主体。 此行为再次类似于 C 语言 **开关** / **情况下** 的行为。 如果 **\* 默认** 构造存在，则它必须出现在所有 **\* 事例** 条目的最后。

如果参数允许 PICKMANY，则会在快照中显示多个 **\* Case** 构造的内容。 这种情况可能会导致相同构造或属性的多个定义。 此类多个定义的处理方式就像它们显式显示在任何 **\* 开关** / **\* Case** 构造之外的 GDL 文件中。 如果多个事例构造共享同一正文，而在配置中命名了多个 **\* 事例**，则正文的内容将仅出现一次。

如果未在配置中命名任何 **\* Case** 构造，则使用 **\* 默认** 构造的内容。 如果未定义 **\* 默认** 构造，则将从快照中排除整个 **\* Switch** / **\* Case** 构造及其所有子代条目。

如果定义了多个同级 **\* 交换机** / **\* 用例** 构造，则每个结构都单独进行计算。 同级构造的合并不适用于 **\* Switch** / **\* Case** 构造。

**\* Switch** 和 **\* 构造** 指令永远不会出现在快照中，因此，在快照中， **\* Case** 构造的子项显示为 **\* Switch** 构造的父项的子项。

在下面的代码示例中，将一个 *Today* 参数定义为一周中的某天。 该示例显示两个同级 **\* Switch** / **\* Case** 构造; 这两个构造分别进行评估。

```GDL
*Schedule:
{
  *Switch: Today
  {
    *Case: Saturday
    *Case: Sunday
    {
 *Eat: Breakfast, Dinner
    }
    *Case: Monday
    *Case: Wednesday
    *Case: Friday
    {
        *Eat: Lunch
    }
  }
  *Switch: Today
  {
    *Case: Sunday
    {
        *ToDo: Laundry
    }
    *Case: Saturday
    {
        *ToDo: Ballgame
    }
    *Default:
    {
        *ToDo: FixBugs
    }
    }
}
```

如果配置指定 `Today: Saturday` ，则快照将包含以下代码。

```GDL
*Schedule:
{
 *Eat: Breakfast, Dinner
  *ToDo: Ballgame
}
```

如果配置指定 `Today: Wednesday` ，则快照将包含以下代码。

```GDL
*Schedule:
{
  *Eat: Lunch
  *ToDo: FixBugs
}
```

如果配置指定 `Today: Tuesday` ，则快照将包含以下代码。

```GDL
*Schedule:
{
  *ToDo: FixBugs
}
```

下面的代码示例演示两个嵌套的 **\* Switch** / **\* Case** 构造。

```GDL
*Schedule:
{
  *Switch: Today
  {
    *Case: Sunday
    {
      *Switch: Weather
      {
        *Case: Sunny
        {
            *ToDo: Garden
        }
        *Case: Cloudy
        {
            *ToDo: Laundry
        }
      }
    }
    *Case: Saturday
    {
      *ToDo: Ballgame
    }
      *Default:
      {
        *ToDo: FixBugs
      }
    }
}
```

 

 




