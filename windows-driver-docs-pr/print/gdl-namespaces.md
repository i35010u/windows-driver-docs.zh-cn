---
title: GDL 命名空间
description: GDL 命名空间
ms.assetid: 111bc393-a44a-4c42-98ef-36f6f225b8a0
keywords:
- GDL WDK，命名空间
- 命名空间 WDK GDL
- 命名空间 WDK GDL，示例
- 未命名的命名空间 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e03a3f2ad6a91d8c2bf6d84159bf08710d1374d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335281"
---
# <a name="gdl-namespaces"></a>GDL 命名空间


GDL 分析器将不允许具有相同名称的多个定义的模板。 两个独立编写模板文件可以无意中使用的模板相同的名称，并阻止 GDL 文件中包括两个模板文件。

若要避免名称冲突问题，GDL 支持命名空间。 标头文件的作者可以指定每个模板和宏的定义应括在中的整个定义属于哪个命名空间\*DefineInNameSpace 构造。 会将其作为此构造的实例名称将成为该命名空间的符号的所有包含定义将要加入。 如果定义位于两个或多个嵌套\*DefineInNameSpace 构造，它将仅属于命名空间定义的最内层\*DefineInNameSpace 构造。 如果定义不能驻留在任何\*DefineInNameSpace 构造，它将分配给默认值或"未命名"命名空间。

如果项包含的模板或宏构造正文放在独立\*DefineInNameSpace 构造，分析器将未放置这些各项新的命名空间因为各项不是单独的定义，因此它们不能位于不同的命名空间。 宏块允许嵌套的宏定义和这些嵌套的定义可以分配给其他命名空间。 但是，更改嵌套定义的命名空间不会扩展其生存期。 仅在定义中的嵌套级别中，可以引用嵌套的宏定义。

命名空间中限定或未限定窗体中，可以引用模板或宏名称。 要使用模板或宏名称，命名空间名称只需前缀使用中间的冒号字符的模板或宏名称 (例如， *Namespace*:*MacroName*)。

**请注意**  提供的值的符号名称\*模板，\*宏，或\*BlockMacro 定义不能由命名空间限定。 定义的命名空间可以定义只能通过使用\*DefineInNameSpace。

 

例如，名为"NSName"的命名空间中定义了名为"TEMPNAME"的模板后，该模板可以引用另一个模板定义通过使用命名空间限定窗体，如以下代码示例所示。

```cpp
*DefineInNameSpace: NSName
{
    *Template:  TEMPNAME
    {
        *%  member attributes
    }
}
```

此模板现在可以从另一个模板使用的命名空间限定语法，如以下代码示例所示引用。

```cpp
*Template:  ANOTHER_TEMPLATE
{
    *Inherits: NSName:TEMPNAME
}
```

如果大多数模板引用将引用同一个命名空间或如果两个或多个命名空间内引用的模板名称之间没有名称冲突，则可忽略的命名空间限定符并仅提供的模板名称并依赖于若要搜索命名空间的列表，直至找到匹配的模板的分析器。

命名空间的列表指定的封闭内的一个或多个 GDL 条目\*UsingNameSpace 构造。 如果任何这些条目包含对模板或宏的非限定的引用，请将受这些引用的解析\*UsingNameSpace 构造。 此构造的实例名称中提供的符号标识要在其中搜索的命名空间。

可以通过嵌套多个构造来指定多个命名空间。 搜索顺序启动最里层\*UsingNameSpace 构造和向外继续。 如果指定的命名空间中找到模板定义，则使用搜索将停止，该模板。 如果没有匹配项找到搜索完所有显式指定的命名空间后，分析器将在每个封闭中搜索名为的命名空间\*DefineInNameSpace 构造从最内层构造向外。 如果搜索未能解析的引用，它将尝试搜索"未命名"命名空间。

**请注意**  如果你需要隔离从外部影响的命名空间搜索顺序，所有所需解析引用的命名空间应指定通过使用\*UsingNameSpace 构造。

 

不应依赖\*DefineInNameSpace 构造来建立搜索顺序，因为该主机可能会环绕所包含的文件的其他\*UsingNameSpace 构造并将搜索的主机指定的命名空间之前由命名的命名空间\*DefineInNameSpace 构造。

例如的模板，定义前面显示两个命名空间具有已显式指定要用于模板的名称解析。 通过名为任何命名空间\*UsingNameSpace 必须之前已定义的\*DefineInNameSpace。 例外情况是"未命名"命名空间，它始终存在，并且由 NULL 符号。

下面的代码示例演示如何指定要定义的搜索顺序的"未命名"命名空间。

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

在前面的示例中，显式指定的命名空间中的所有搜索已都失败，但该示例显式指定 NSName2 命名空间之前搜索的"未命名"命名空间后，将搜索"未命名"命名空间。

因为 GDL 数据条目永远不会显式引用模板名称，使用\*UsingNameSpace 不会影响哪些模板分配给每个数据条目。 但是，命名空间搜索顺序\*UsingNameSpace 指定 （这有效的第一个 GDL 数据条目进行分析时) 中搜索根模板使用。 如果包含一个或多个 GDL 标头文件，应确保它们确实无意中受到第一个定义数据输入，并因此确定哪个命名空间用于查找根模板。

**请注意**  宏定义是作用域受限的封闭的嵌套级别。 但是，命名空间的嵌套级别不限制宏定义的作用域，因为不需要定义一个宏来属于特定命名空间，如果宏的范围是不足够大，无法在该命名空间外可见。

 

可以构造其他类型之间交错 Namespace 构造。 没有几乎无限制的命名空间构造可以出现的位置。 非命名空间构造不会影响命名空间解析。

 

 




