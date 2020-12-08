---
title: 数组模板数据类型
description: 数组模板数据类型
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，复合
- 数组数据类型 WDK GDL
- ElementType 指令 WDK GDL
- RequiredDelimiter 指令 WDK GDL
- OptionalDelimiter 指令 WDK GDL
- ElementTags 指令 WDK GDL
- 数组大小指令 WDK GDL
- ArrayLabel 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24586bcd997cacd83d45517f1b6076d4e840b44b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836161"
---
# <a name="array-template-data-types"></a>数组模板数据类型


数组数据类型由一个或多个具有相同数据类型的值组成。 数组可以定义为固定、可变或无限长度。

**\* 数据类型：数组** 指示一个模板定义一种复合数据类型，该类型的成员均为同一数据类型 (也称为成员的数据类型) 。 数组数据类型的成员将输出为属于表示封闭上下文的元素的单个 XML 子元素。

如果每个子元素都表示一个数据类型基元，则数据类型将由每个元素中的 XML 属性 **xsi： type** 定义。 如果将 GDL 属性定义为数据类型数组，则封闭上下文将是 &lt; GDL \_ attribute &gt; 元素。 每个 XML 子元素的元素名称将是 **\* ElementTags** 指令定义的对应标记。 如果复合本身是另一个复合数据类型的成员，则将创建一个元素来表示该封闭上下文。 此父元素的名称将是由定义了封闭复合数据类型的模板分配的相应标记。

以下指令用于定义数组数据类型：

-   **\* ElementType** (必需的) 。 定义所有元素的数据类型的模板的名称。 只能指定一种数据类型。

-   需要) **\* RequiredDelimiter** (。 一个字符串，该字符串在语法上将每个数组元素与下一个数组元素分隔开来。 两个连续分隔符将被解释为省略的元素。 分隔符不需要指示省略尾随元素。 如果使用空格作为分隔符或作为分隔符字符串的一部分，则应非常小心。 例如，由分析器将多余的空格字符解释为指示省略的元素;而且，由于您可能无法看到这样的额外空白字符，您可能会遇到意外的分析错误。

    此外，还会从源文件中去除多余的空格，并且通常会将空格作为预处理器、宏和注释处理的结果添加到输入流。 因此，分析的实际字符串可能与最初指定的空间字符数量完全不同。

    不应使用制表符作为必需的分隔符字符串的一部分，因为在输入处理期间，它们会定期转换为空格字符。

-   **\* OptionalDelimiter** (可选) 。 任何包含在 **\* OptionalDelimiter** 中指定的和出现在 **\* RequiredDelimiter** 字符串旁边的字符的字符串都将被视为分隔符部分。 在 **\* RequiredDelimiter** 字符串中定义的第一个字符不得出现在 **\* OptionalDelimiter** 中。

-   需要) **\* ElementTags** (。 如果希望为数组中的每个元素分配相同的元素名称 (或者数组的大小不受限制) ，请仅提供一个标记。 否则，请提供一个等于 **\* 数组大小** 指定的最大值的数字。

    数组的每个成员都将用相应的标记命名。 如果省略了一个或多个数组元素，此命名会很有用。 如果省略数组元素，则不使用与省略的元素对应的标记。 若要避免对客户端造成混淆，请不要将 GDL 快照保留元素名称 (为、构造、特性和个性 ) 为标记名称。

-   需要) **\* 数组大小** (。 使用一个整数指定固定大小的数组的大小，或使用两个整数指定可变大小数组的最小和最大允许大小。 请注意，最小大小允许使用零，GPD 通配符 (\*) 可用于指定大小或最大大小。 用连续的逗号表示实例数据中的省略值 (例如 `*DaysOfWeek: (Sunday, Monday,  ,  Wednesday,  , Friday,`) 。

-   **\* ArrayLabel** (可选) 。 如果指定了此指令，数组元素列表必须用圆括号括起来，并以 **\* ArrayLabel** 标签开头。 如果未在此指令中指定标签，则括号是可选的，不允许使用任何内标签。

请考虑以下模板。

```GDL
*Template:  RECTANGLE
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  INTEGER
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ArrayLabel: "rect"
    *ElementTags: (left, top, right, bottom)
    *ArraySize: 4
}
```

此模板定义固定大小的、四个整数的数组。 为数组分配了一个 () 的标签 `rect` ，并为数组中的每个元素分配一个唯一的元素标记。 这些标记会在 XML 输出中标记每个元素，以帮助客户端。 每个元素都由逗号或逗号以及空格和制表符的任意组合彼此分隔。 由于数组大小是固定的，因此不允许任何元素省略。

**\* DATATYPE：数组** 模板不生成相应的架构。 改为使用 **\* ElementType** 指令中命名的模板的架构。

请考虑以下 GDL 条目。

```GDL
*ImageableArea:   rect( - 10, 20 , +30, 0x40  )  
```

并考虑 IMAGERECT 模板。

```GDL
*Template:  IMAGERECT
{
    *Name:  "*ImageableArea"
    *Type:  ATTRIBUTE
    *ValueType:  RECTANGLE
}
```

如果 GDL 项由 IMAGERECT 模板解释，则生成的 XML 输出将为。

```xml
<GDL_ATTRIBUTE Name="*ImageableArea"  >
<left  xsi:type="GDLW_int">-10</left>
   <top  xsi:type="GDLW_int">20</top>
   <right  xsi:type="GDLW_int">30</right>
   <bottom  xsi:type="GDLW_int">64</bottom>
</GDL_ATTRIBUTE> 
```

请注意，引用是 **GDLW \_ int** 类型的包装类型，而不是原始 **int**。
