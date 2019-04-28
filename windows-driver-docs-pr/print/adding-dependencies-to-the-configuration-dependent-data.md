---
title: 将依赖项添加到配置相关的数据
description: 将依赖项添加到配置相关的数据
ms.assetid: 16e15147-6e83-4675-b050-cf13dcd6b397
keywords:
- GDL WDK 配置
- 配置 WDK GDL，添加依赖项
- 将依赖项添加到配置依赖于数据 WDK GDL
- 配置依赖于数据 WDK GDL 中的依赖关系
- 开关/用例指令 WDK GDL
- 功能/选项指令 WDK GDL
- 构造 WDK GDL，默认构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7a5ad83041e6a5b425f423676395eaf28d79e9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343171"
---
# <a name="adding-dependencies-to-the-configuration-dependent-data"></a>将依赖项添加到配置相关的数据


**\*交换机**/**\*用例**指令进行数据依赖于使用定义的参数**\*功能** / **\*选项**指令。 构造标记**\*交换机**构造名称中定义的参数之一**\*功能**构造。 由构造标记的参数的引用**\*交换机**构造可能通过定义前面**\*功能**构造。

正文**\*交换机**构造包含大量**\*用例**构造和一个可选**\*默认**构造。 任何其他子项可以出现在**\*交换机**构造。 构造标记**\*用例**构造名称中定义的允许值之一**\*选项**对应中命名的参数的构造**\*交换机**构造。 不用于构造标记<strong>\*默认</strong>构造。

**\*交换机**构造可以显示为任何其他构造中的子项，只不过**\*交换机**构造不能为另一个子**\*开关**构造。 正文**\*用例**构造可包含任何 GDL 条目，除**\*用例**构造不能为的祖先**\*功能**或**\*默认**构造。

**\*交换机**/**\*用例**指令的工作方式与 C 语言构造具有相同名称的非常类似。 任何的内容**\*用例**构造 (其构造标记命名配置中为当前值或命名参数状态**\*开关**构造） 允许在快照中出现。 否则，分析器可防止生成中包含的项**\*用例**构造使其不显示在快照中。

**请注意**  与不同 C 版本**\*交换机**/**\*用例**，GDL 不需要停止执行从一个 break 语句继续末尾**\*用例**构造。

 

如果的正文<strong>\*用例</strong>省略构造 (即**\*用例**显示为一个属性而不是一种构造)，接下来的正文 **\*用例**或**\*默认**将使用构造。 此行为也类似于 C 语言中的行为**交换机**/**用例**。 如果**\*默认**构造存在，则它必须显示最后一个，毕竟**\*用例**条目。

如果该参数允许 PICKMANY，多个内容**\*用例**构造可以出现在快照中。 这种情况下可能会导致同一构造或属性的多个定义。 此类的多个定义的处理就像显式之外任何 GDL 文件中出现**\*交换机**/**\*用例**构造。 如果多个**\*用例**构造共享相同的主体和多个名为在配置中，正文的内容将仅出现一次。

如果没有**\*用例**中配置的内容命名构造**\*默认**使用构造。 如果没有**\*默认**定义构造，则整个**\*开关**/**\*用例**构造和所有其从快照中排除子代的条目。

如果多个同级**\*交换机**/**\*用例**定义了构造，每个计算相互独立。 构造同级的合并不适用于**\*交换机**/**\*用例**构造。

**\*交换机**和**\*构造**指令不会显示在快照，因此，在快照的子项**\*用例**构造显示为父级的子项**\*交换机**构造。

在下面的代码示例中，*今天*参数定义为采用的星期日期。 该示例演示两个同级**\*交换机**/**\*用例**构造; 这两个将独立进行计算。

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

如果配置指定`Today: Saturday`，快照将包含下面的代码。

```GDL
*Schedule:
{
 *Eat: Breakfast, Dinner
  *ToDo: Ballgame
}
```

如果配置指定`Today: Wednesday`，快照将包含下面的代码。

```GDL
*Schedule:
{
  *Eat: Lunch
  *ToDo: FixBugs
}
```

如果配置指定`Today: Tuesday`，快照将包含下面的代码。

```GDL
*Schedule:
{
  *ToDo: FixBugs
}
```

下面的代码示例演示两个嵌套**\*交换机**/**\*用例**构造。

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

 

 




