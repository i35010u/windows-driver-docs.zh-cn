---
title: 复合模板数据类型
description: 复合模板数据类型
ms.assetid: 5fd9218a-2827-4cca-b913-eeb6484653d9
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，复合
- 复合数据类型 WDK GDL
- ElementType 指令 WDK GDL
- RequiredDelimiter 指令 WDK GDL
- OptionalDelimiter 指令 WDK GDL
- ElementTags 指令 WDK GDL
- ArraySize 指令 WDK GDL
- ArrayLabel 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24943c647dca4a7a9fd0ab7dd5f414ad7d0bb39e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556028"
---
# <a name="composite-template-data-types"></a>复合模板数据类型


复合数据类型由一个或多个具有相同或不同的数据类型的值组成。 复合可以固定或变量 （而不是无限期） 长度。 此数据类型为类似于 C lLanguage 结构数据类型。

**\*数据类型：复合**指示一个模板来定义其成员可以是不同的数据类型的复合数据类型。 复合数据类型的成员将输出作为属于表示封闭上下文元素的单个 XML 子元素。 如果每个子元素表示的数据类型的基元，将由 XML 特性定义的数据类型**xsi: type**中每个元素。 如果 GDL 属性被定义为**数据类型：复合**，则将封闭上下文&lt;GDL\_属性&gt;元素。 每个 XML 子元素的元素名称将是相应的标记由定义**指令：\*ElementTags**。

如果复合本身另一种复合数据类型的成员，则将创建一个元素来表示该封闭上下文。 此父元素的名称将是相应的标记分配到封闭的复合数据类型相对应的模板。

以下指令用于定义的复合数据类型：

-   **\*ElementType** （必需）。 定义数据类型的每个元素的模板的名称。 必须为每个元素指定一种数据类型。 一个或多个元素可以具有相同的数据类型。 提供的 ElementTypes 数应等于 ArraySize 或最大值 **\*ArraySize**指定。

-   **\*RequiredDelimiter** （必需）。 一个字符串，语法上将从下一步中分隔每个组合元素。 两个连续的分隔符将被解释为省略的元素。 不需要分隔符来指示尾随元素省略。

    你应非常小心，如果使用空格作为分隔符或作为分隔符字符串的一部分。 例如，分析器会将多余的空格字符解释为指示省略元素;并且因为您可能看不到额外的空格，可能发生奇怪分析错误。 此外，从源文件定期去除多余的空格，空格通常添加到由于预处理器、 宏和注释处理的输入流。 因此，进行分析的实际字符串可能具有完全不同数量的空间比原始指定的字符。 因为它们会定期转换为空格字符在输入的处理期间，不应作为所需的分隔符字符串的一部分使用的制表符字符数。

-   **\*OptionalDelimiter** （可选）。 中指定的字符组成的任何字符串 **\*OptionalDelimiter**显示与相邻 **\*RequiredDelimiter**字符串将被视为的一部分分隔符。

-   **\*ElementTags** （必需）。 提供的标记数应等于 ArraySize 或最大值 **\*ArraySize**指定。 每个成员将使用相应的标记来标记。 此标记非常有用，如果省略了一个或多个元素。 如果省略了复合元素，不是使用省略元素对应的标记。 为了避免混淆客户端，请为标记名称使用 GDL 快照保留元素名称。 这些保留的名称为构造、 特性和个性。

-   **\*ArraySize** （可选）。 如果省略此指令，则将假定一个固定大小复合。 大小是与模板中的名称数相等 **\*ElementType**。

    使用两个整数来指定最小值和最大允许大小可变的复合。 请注意，零允许的最小大小。 不允许的大小无限制的复合数据类型。 不能使用 GPD 通配符字符 (\*) 指定的大小或最大大小。

-   **\*ArrayLabel** （可选）。 如果指定此指令，则复合元素的列表必须用括号括起来，前面加上 **\*ArrayLabel**标签。 如果在此指令中不指定任何标签，括号是可选的并允许任何前置的标签。

请考虑以下模板。

```cpp
*Template:  QUALNAME_EX
{
    *Type:  DATATYPE
    *DataType:   COMPOSITE
    *ElementType: (SYMBOL, SYMBOL, INTEGER)
    *RequiredDelimiter: "."
    *ElementTags: (feature, option, resourceID)
}
```

前面的模板定义固定大小，复合的两个符号数据类型和一个整数。 复合未标记。 复合中的每个元素分配唯一 ElementTag。 这些标记标签将 XML 输出，以帮助客户端中的每个元素。 每个元素彼此分离且只有一个句点 （.）;任何其他字符被不视为分隔符的一部分。 **\*ArraySize**未指定，因此假定固定的大小。 元素的总大小固定的因为允许没有成员省略。

**\*数据类型：复合**模板不会生成相应的架构。 中命名的模板的架构 **\*ElementType**改为使用指令。

例如，请考虑按以下方式定义的符号模板。

```cpp
*Template:  SYMBOL
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "SYMBOLNAME"
}
```

并考虑以下 GDL 条目。

```cpp
*rcNameID:     ( RESDLL.stdname.467 )  
```

或者，考虑以下 GDL 条目没有可选的括号。

```cpp
*rcNameID:     RESDLL.stdname.467 
```

假设使用以下 RC 解释 GDL 条目\_名称\_ID 模板。

```cpp
*Template:  RC_NAME_ID
{
    *Name:  "*rcNameID"
    *Type:  ATTRIBUTE
    *ValueType:  QUALNAME_EX
    *Additive: LEAST_TO_MOST_RECENT
}
```

生成的 XML 输出将如下所示。

```cpp
    <GDL_ATTRIBUTE Name="*rcNameID"  >
        <feature  xsi:type="GDLW_string">RESDLL</feature>
        <option  xsi:type="GDLW_string">stdname</option>
        <resourceID  xsi:type="GDLW_int">467</resourceID>
    </GDL_ATTRIBUTE>
```

下面的示例通过使用保存的日期数据类型，表示时间间隔对时间间隔数据类型显示嵌套的复合数据类型。 每个日期数据类型是月、 日和年的数据类型的组合。 休假 GDL 属性使用的时间间隔数据类型来表达某位员工可能不会出现的时间段。 以下集合的模板将完成这种情况。

### <a name="month-template"></a>月模板

```cpp
*Template:  MONTHS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "months"
    *EnumeratorList: (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec)
}
```

### <a name="day-template"></a>一天模板

```cpp
*Template:  DAY
{
*Inherits: INTEGER
*MinValue: 1
*MaxValue: 31
}
```

### <a name="year-template"></a>年模板

```cpp
*Template:  YEAR
{
*Inherits: INTEGER
*MinValue: 1900
*MaxValue: 2100
}
```

### <a name="date-template"></a>日期模板

```cpp
*Template:  DATE
{
    *Type:  DATATYPE
    *DataType:   COMPOSITE
    *ElementType: (MONTHS, DAY, YEAR)
    *RequiredDelimiter: "-"
    *ElementTags: (month, day, year)
}
```

### <a name="interval-template"></a>间隔模板

```cpp
*Template:  INTERVAL
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  DATE
    *RequiredDelimiter: "to"
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (start_date, end_date)
    *ArraySize: 2
}
```

### <a name="vacation-template"></a>休假模板

```cpp
*Template:  VACATION
{
    *Name:  "*VacationDates"
    *Type:  ATTRIBUTE
    *ValueType:  INTERVAL
}
```

请考虑以下 GDL 条目。

```cpp
*VacationDates:  Dec-20-2001 to Jan-3-2002
```

如果该项 GDL 解释使用休假模板中，生成的 XML 输出将如下所示。

```cpp
    <GDL_ATTRIBUTE Name="*VacationDates"  >
        <start_date >
            <month  xsi:type="GDLW_months">Dec</month>
            <day  xsi:type="GDLW_int">20</day>
            <year  xsi:type="GDLW_int">2001</year>
        </start_date>
        <end_date >
            <month  xsi:type="GDLW_months">Jan</month>
            <day  xsi:type="GDLW_int">3</day>
            <year  xsi:type="GDLW_int">2002</year>
        </end_date>
    </GDL_ATTRIBUTE>
```

 

 




