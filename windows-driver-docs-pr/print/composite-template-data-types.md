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
- 数组大小指令 WDK GDL
- ArrayLabel 指令 WDK GDL
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 12e7e1054c29bb407b2e9ddd50950d5d17f8477f
ms.sourcegitcommit: 88f6e7355de9e0714057020557dc8c7831e90e7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2020
ms.locfileid: "84638441"
---
# <a name="composite-template-data-types"></a>复合模板数据类型

复合数据类型由一个或多个具有相同或不同数据类型的值组成。 复合可以具有固定的或可变的（但非无限）长度。 此数据类型类似于 C lLanguage 结构数据类型。

** \* 数据类型：复合**指示模板定义其成员可以是不同数据类型的复合数据类型。 复合数据类型的成员将输出为属于表示封闭上下文的元素的单个 XML 子元素。 如果每个子元素都表示一个数据类型基元，则数据类型将由每个元素中的 XML 属性**xsi： type**定义。 如果将 GDL 属性定义为**DataType：复合**，则封闭上下文将是 &lt; GDL \_ attribute &gt; 元素。 每个 XML 子元素的元素名称将是** \* ElementTags**定义的相应标记。

如果复合本身是另一个复合数据类型的成员，则将创建一个元素来表示该封闭上下文。 此父元素的名称将是对应于所包含的复合数据类型的模板分配的对应标记。

以下指令用于定义复合数据类型：

- ** \* ElementType** （必需）。 定义每个元素的数据类型的模板的名称。 必须为每个元素指定一种数据类型。 一个或多个元素可以具有相同的数据类型。 提供的 ElementTypes 数应等于** \* 数组大小**指定的数组大小或 Max 值。

- ** \* RequiredDelimiter** （必需）。 在语法上将每个复合元素与下一个组合元素分隔的字符串。 两个连续分隔符将被解释为省略的元素。 分隔符不需要指示省略尾随元素。

    如果使用空格作为分隔符或作为分隔符字符串的一部分，则应该非常小心。 例如，分析器会将多余的空格字符解释为指示省略的元素;由于你可能看不到额外的空白，因此可能会出现奇怪的分析错误。 此外，还会从源文件中去除多余的空格，并且通常会将空格作为预处理器、宏和注释处理的结果添加到输入流。 因此，分析的实际字符串可能与最初指定的空间字符数量完全不同。 不应使用制表符作为必需的分隔符字符串的一部分，因为在输入处理期间，它们会定期转换为空格字符。

- ** \* OptionalDelimiter** （可选）。 包含在** \* OptionalDelimiter**中指定的字符的任何字符串都出现在** \* RequiredDelimiter**字符串旁边，将被视为分隔符的一部分。

- ** \* ElementTags** （必需）。 提供的标记数应等于** \* 数组大小**指定的数组大小或 Max 值。 每个成员都将用相应的标记进行标记。 如果省略了一个或多个元素，则此标记很有用。 如果省略复合元素，则不使用与省略的元素对应的标记。 若要避免混淆客户端，请不要将 GDL 快照保留元素名称用作标记名称。 这些保留名称为构造、属性和个性。

- ** \* 数组大小**（可选）。 如果省略该指令，则假定为固定大小的组合。 大小将等于** \* ElementType**中的模板名称数。

    使用两个整数指定可变大小的复合的最小和最大允许大小。 请注意，最小大小允许使用零。 不允许使用无限制大小的组合数据类型。 不能使用 GPD 通配符（ \* ）来指定大小或最大大小。

- ** \* ArrayLabel** （可选）。 如果指定了此指令，则必须用括号将复合元素列表括起来，并以** \* ArrayLabel**标签开头。 如果未在此指令中指定标签，则括号是可选的，不允许使用任何内标签。

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

前面的模板定义固定大小的、两个符号数据类型和一个整数的组合。 复合未标记。 复合中的每个元素均分配有一个唯一的 ElementTag。 这些标记会在 XML 输出中标记每个元素，以帮助客户端。 每个元素都与下一个句点（.）分隔，不会将其他字符视为分隔符的一部分。 未指定** \* 数组大小**，因此假定为固定复合大小。 由于复合大小是固定的，因此不允许任何成员省略。

** \* DATATYPE：复合**模板不生成相应的架构。 改用** \* ElementType**指令中命名的模板的架构。

例如，请考虑定义如下的符号模板。

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

或者，请考虑以下不带可选括号的 GDL 项。

```cpp
*rcNameID:     RESDLL.stdname.467
```

假设使用以下 RC \_ NAME ID 模板解释 GDL 条目 \_ 。

```cpp
*Template:  RC_NAME_ID
{
    *Name:  "*rcNameID"
    *Type:  ATTRIBUTE
    *ValueType:  QUALNAME_EX
    *Additive: LEAST_TO_MOST_RECENT
}
```

生成的 XML 输出如下所示。

```cpp
    <GDL_ATTRIBUTE Name="*rcNameID"  >
        <feature  xsi:type="GDLW_string">RESDLL</feature>
        <option  xsi:type="GDLW_string">stdname</option>
        <resourceID  xsi:type="GDLW_int">467</resourceID>
    </GDL_ATTRIBUTE>
```

下面的示例通过使用一个时间间隔数据类型（表示一对表示时间间隔的日期数据类型）来显示嵌套的复合数据类型。 每个日期数据类型都是月、日和年数据类型的组合。 "间隔" 数据类型由 "假期 GDL" 属性用来表示员工可能缺勤的时间段。 以下模板集合将实现这种情况。

## <a name="month-template"></a>月模板

```cpp
*Template:  MONTHS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "months"
    *EnumeratorList: (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec)
}
```

## <a name="day-template"></a>日模板

```cpp
*Template:  DAY
{
*Inherits: INTEGER
*MinValue: 1
*MaxValue: 31
}
```

## <a name="year-template"></a>年份模板

```cpp
*Template:  YEAR
{
*Inherits: INTEGER
*MinValue: 1900
*MaxValue: 2100
}
```

## <a name="date-template"></a>日期模板

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

## <a name="interval-template"></a>间隔模板

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

## <a name="vacation-template"></a>休假模板

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

如果使用假期模板解释此 GDL 条目，则生成的 XML 输出将如下所示。

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
