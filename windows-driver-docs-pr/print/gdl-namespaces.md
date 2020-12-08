---
title: GDL 命名空间
description: GDL 命名空间
keywords:
- GDL WDK，命名空间
- 命名空间 WDK GDL
- 命名空间 WDK GDL，示例
- 未命名命名空间 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcabf2b3557d148cf6702e298426dc4c9447eea8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796981"
---
# <a name="gdl-namespaces"></a>GDL 命名空间


GDL 分析器将不允许多次定义同名的模板。 两个独立编写的模板文件可能会无意中将同一名称用于模板，并阻止你在 GDL 文件中包含这两个模板文件。

为了避免名称冲突问题，GDL 支持命名空间。 标头文件的作者可以通过在 DefineInNameSpace 构造中包含整个定义来指定每个模板和宏定义应属于的命名空间 \* 。 作为此构造的实例名称提供的符号将成为所包含的所有定义将属于的命名空间。 如果定义位于两个或更多个嵌套的 \* DefineInNameSpace 构造中，则它将仅属于由最内层 DefineInNameSpace 构造定义的命名空间 \* 。 如果定义不在任何 \* DefineInNameSpace 构造中，则会将其分配给默认命名空间或 "未命名" 命名空间。

如果包含模板或宏构造主体的项包含在单独的 \* DefineInNameSpace 构造中，则分析器不会将这些项放入新的命名空间，因为单个项不是单独的定义，因此它们不能在不同的命名空间中。 块宏允许嵌套宏定义，这些嵌套的定义可以分配给其他命名空间。 但是，更改嵌套定义的命名空间不会扩展其生存期。 嵌套宏定义只能在定义它的嵌套级别内引用。

可在命名空间中以限定或非限定形式引用模板或宏名称。 若要限定模板或宏名称，命名空间名称只需加上一个带引号字符 (例如， *命名空间*：*MacroName*) 。

**注意**   作为 \* 模板、宏或 BlockMacro 定义的值提供的符号名称 \* \* 不能由命名空间限定。 只能使用 DefineInNameSpace 定义定义的命名空间 \* 。

 

例如，在名为 "NSName" 的命名空间中定义了一个名为 "TEMPNAME" 的模板之后，可以通过使用命名空间限定的格式，另一个模板定义引用该模板，如以下代码示例所示。

```cpp
*DefineInNameSpace: NSName
{
    *Template:  TEMPNAME
    {
        *%  member attributes
    }
}
```

现在可以通过使用命名空间限定语法从另一个模板引用此模板，如以下代码示例所示。

```cpp
*Template:  ANOTHER_TEMPLATE
{
    *Inherits: NSName:TEMPNAME
}
```

如果大多数模板引用将引用相同的命名空间，或者在两个或更多命名空间内引用的模板名称之间没有名称冲突，则可以省略命名空间限定符并仅提供模板名称，并依赖分析器搜索命名空间列表，直到找到匹配的模板。

命名空间列表通过在 UsingNameSpace 构造中包含一个或多个 GDL 项来指定 \* 。 如果其中任何一项包含对模板或宏的非限定引用，则这些引用的分辨率将受到 \* UsingNameSpace 构造的影响。 作为此构造的实例名称提供的符号标识要搜索的命名空间。

可以通过嵌套若干构造来指定多个命名空间。 搜索顺序从最内部的 \* UsingNameSpace 构造开始，并继续向外。 如果在指定的命名空间中找到了模板定义，则搜索将停止，并使用该模板。 如果在搜索了所有显式指定的命名空间后未找到匹配项，则分析器将从最内层构造向外搜索每个封闭 DefineInNameSpace 构造中命名的命名空间 \* 。 如果该搜索未能解析引用，它将尝试搜索 "未命名" 命名空间。

**注意**   如果需要将命名空间搜索顺序与外部影响隔离，则应使用 UsingNameSpace 构造来指定解析引用所需的所有命名空间 \* 。

 

您不应依赖于 \* DefineInNameSpace 构造来建立搜索顺序，因为宿主可能会将包含的文件与附加的 \* UsingNameSpace 构造包围在一起，并将在 DefineInNameSpace 构造命名的命名空间之前搜索主机指定的命名空间 \* 。

例如，先前定义的模板显示了两个命名空间，它们已显式指定为用于模板名称解析。 由 UsingNameSpace 命名的任何命名空间都 \* 必须之前由 DefineInNameSpace 定义 \* 。 "未命名" 命名空间是 "未命名" 命名空间，该命名空间始终存在并且由 NULL 符号命名。

下面的代码示例演示如何指定 "未命名" 命名空间来定义搜索顺序。

```cpp
*UsingNameSpace: NSName2
{
    *UsingNameSpace:  *%%%%%  omitting symbol specifies the  Unnamed 
*%  Namespace.
    {
        *UsingNameSpace: NSName
        {
            *Template:  ANOTHER_TEMPLATE
            {
                *Inherits: TEMPNAME
            }
        }
    }
}
```

在前面的示例中，将在显式指定的命名空间中的所有搜索均已失败之后搜索 "未命名" 命名空间，但该示例显式指定在 NSName2 命名空间之前搜索 "未命名" 命名空间。

由于 GDL 数据项从不显式引用模板名称，使用 \* UsingNameSpace 将不会影响分配给每个数据输入的模板。 但是，UsingNameSpace 的命名空间搜索顺序指定了在 \* 分析第一个 GDL 数据输入时生效的 (，) 用于搜索根模板。 如果包含一个或多个 GDL 头文件，则应确保这些文件不会无意中变成第一个定义数据输入，从而确定用于查找根模板的命名空间。

**注意**   宏定义由封闭嵌套级别限制作用域。 但是，命名空间嵌套级别不会限制宏定义的作用域，因为如果宏的作用域不够大，无法在该命名空间之外显示，则不需要将宏定义为属于特定的命名空间。

 

命名空间构造可以在其他类型的构造之间隔行扫描。 对于命名空间构造的出现位置，几乎没有任何限制。 非命名空间构造不影响命名空间解析。

 

 




