---
title: 数组模板数据类型
description: 数组模板数据类型
ms.assetid: d6be4ec3-1980-4e55-bd52-5249cd93deb8
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，复合
- 数组数据类型 WDK GDL
- ElementType 指令 WDK GDL
- RequiredDelimiter 指令 WDK GDL
- OptionalDelimiter 指令 WDK GDL
- ElementTags 指令 WDK GDL
- ArraySize 指令 WDK GDL
- ArrayLabel 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e06ad4d5b2c8ab9ccac6f4ba3267cc02e1f4c8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543807"
---
# <a name="array-template-data-types"></a>数组模板数据类型


数组数据类型由一个或多个值，所有具有相同的数据类型。 数组可以定义为固定变量，或无限期长度。

**\*数据类型：数组**指示一个模板来定义其成员都是相同的数据类型 （也称为成员的数据类型） 的复合数据类型。 数组数据类型的成员将输出作为属于表示封闭上下文元素的单个 XML 子元素。

如果每个子元素表示的数据类型的基元，将由 XML 特性定义的数据类型**xsi: type**中每个元素。 如果 GDL 属性定义为数据类型数组，将是封闭上下文&lt;GDL\_属性&gt;元素。 每个 XML 子元素的元素名称将是相应标记的 **\*ElementTags**指令定义。 如果复合本身另一种复合数据类型的成员，则将创建一个元素来表示该封闭上下文。 此父元素的名称将是相应的标记由定义的封闭的复合数据类型的模板分配。

以下指令用于定义数组数据类型：

-   **\*ElementType** （必需）。 定义数据类型的所有元素的模板的名称。 可以指定只有一个数据类型。

-   **\*RequiredDelimiter** （必需）。 一个字符串，语法上将从下一步中分隔每个数组元素。 两个连续的分隔符将被解释为省略的元素。 不需要分隔符来指示尾随元素省略。 要非常小心，如果使用空格作为分隔符或分隔符字符串的一部分。 例如，多余的空格字符将被当做分析器，该值指示省略元素;因为不可能能够看到此类额外空白字符，可能会遇到意外的分析错误。

    此外，从源文件定期去除多余的空格，空格通常添加到由于预处理器、 宏和注释处理的输入流。 因此，进行分析的实际字符串可能具有完全不同数量的空间比原始指定的字符。

    因为它们会定期转换为空格字符在输入的处理期间，不应作为所需的分隔符字符串的一部分使用的制表符字符数。

-   **\*OptionalDelimiter** （可选）。 中指定的字符组成的任何字符串 **\*OptionalDelimiter**支持并出现与相邻 **\*RequiredDelimiter**字符串将被视为部分分隔符。 在中定义的第一个字符 **\*RequiredDelimiter**字符串中不能出现 **\*OptionalDelimiter**。

-   **\*ElementTags** （必需）。 如果你想要分配相同的元素名称的数组中的每个元素 （或者如果数组可以是不受限制的大小），提供以下只有一个标记。 否则，请提供一个数字的最大值等于 **\*ArraySize**指定。

    数组的每个成员名称将为与相应的标记。 此命名功能非常有用，如果省略了一个或多个数组元素。 如果省略了数组元素，不是使用省略元素对应的标记。 为了避免混淆客户端，请为标记名称使用 GDL 快照保留元素名称 （即，构造、 特性和各自的特点，）。

-   **\*ArraySize** （必需）。 使用一个整数来指定固定大小的数组的大小或使用两个整数来指定最小值和最大允许大小可变的数组的大小。 请注意，零允许的最小大小和 GPD 通配符字符 (\*) 可用于指定的大小或最大大小。 指示使用连续的逗号分隔实例数据中省略的值 (例如， `*DaysOfWeek: (Sunday, Monday,  ,  Wednesday,  , Friday,`)。

-   **\*ArrayLabel** （可选）。 如果指定此指令，则数组元素的列表必须用括号括起来，前面加上 **\*ArrayLabel**标签。 如果在此指令中不指定任何标签，括号是可选的并允许任何前置的标签。

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

此模板定义的四个整数中的固定大小的数组。 数组分配标签 (`rect`) 和数组中的每个元素分配唯一的元素标记。 这些标记标签将 XML 输出，以帮助客户端中的每个元素。 每个元素被分隔与下一个逗号或一个逗号和空格和制表符字符的任意组合。 因为数组大小固定的不允许省略任何元素的方式。

**\*数据类型：数组**模板不会生成相应的架构。 模板中命名的架构 **\*ElementType**改为使用指令。

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

如果 GDL 条目解释 IMAGERECT 模板中，将生成的 XML 输出。

```xml
<GDL_ATTRIBUTE Name="*ImageableArea"  >
<left  xsi:type="GDLW_int">-10</left>
   <top  xsi:type="GDLW_int">20</top>
   <right  xsi:type="GDLW_int">30</right>
   <bottom  xsi:type="GDLW_int">64</bottom>
</GDL_ATTRIBUTE> 
```

请注意，引用将指向已包装的类型**GDLW\_int**而不是原始**int**。
