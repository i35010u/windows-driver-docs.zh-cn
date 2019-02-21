---
title: 多个个人设置模板的数据类型
description: 多个个人设置模板的数据类型
ms.assetid: ee550416-9185-41fa-b113-6a1d22c3aa96
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，复合
- MULTIPLE_PERSONALITY 数据类型 WDK GDL
- ElementType 指令 WDK GDL
- ElementTags 指令 WDK GDL
- 联合 WDK GDL
- GDL WDK 联合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c3d34adb0c002da6fdd019ad85f9e37dd5edce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519351"
---
# <a name="multiple-personality-template-data-types"></a>多个个人设置模板的数据类型


多个\_个性数据类型表示一个值，可以在不同的时间保存不同的数据类型。 此数据类型是类似于 C 语言**union**数据类型。

\*数据类型：多个\_个性指示一个模板来定义可接受值属于多个不同的数据类型，类似于 C 语言的数据类型**union**数据类型。 多个\_个性数据类型会尝试确定标识 （即，数据类型） 的值并将输出相同的 XML，如同在属于标识的数据类型的模板中已明确定义值。 换而言之，如果多个\_个性数据类型已定义用于存储字符串或整数或符号，和实际保持一个整数的值，如果 XML 输出将是对于整数数据类型。

此外发出个性标记属性，以便帮助客户端确定已发出的值的数据类型。 筛选器通过分析通过使用每个潜在的数据类型的值来确定值的数据类型。 选择成功匹配的输入值的最大容量的数据类型。 如果出现数量相同，将选择出现在列表中第一个元素类型。

**请注意**  可以构造值语法，可欺骗此计算算法的计算，所以请小心选择要列出的元素类型时。 类型必须是充分分析算法的不同。 例如，分析器筛选器无法识别任何 XML 语法，因为它无法区分两个 XML\_类型的数据类型。 但是，在这些情况下，在候选数据类型的定义可以包含\*ArrayLabel 有助于区分这些分析器的指令。

 

以下指令用于定义多个\_个性数据类型：

-   \*ElementType （必需）。 定义此值可以假设的潜在的数据类型的模板名称的列表。

-   \*ElementTags （必需）。 标记，以帮助客户端标识实际分配给的值的数据类型的列表。 提供的标记数应等于的中列出的模板数\*ElementType。 标记将出现在生成的 XML 元素表示的值中的个人设置属性。 例如，如果数据类型为多个个人设置数据类型的数组，表示数组的单个成员的元素将包含个性属性。 表示整个数组的元素将不会包含个人设置属性，因为数组本身不具有定义的个性;相反，数组的单个成员具有其自己独特的个性属性值。

请考虑以下模板。

```cpp
*Template:  INT_OR_QUALNAME_EX
{
    *Type:  DATATYPE
    *DataType:   MULTIPLE_PERSONALITY
    *ElementType:  (INTEGER, QUALNAME_EX, QUOTEDSTRING)
    *ElementTags: (integer, QualNameEx, QuotedString)
}
```

此模板定义一个数据类型，可以容纳的整数值，QUALNAME\_EX 值或 QUOTEDSTRING 值。 无论什么数据类型是所选的将使用相应的用户定义 ElementTag 来标识。

请考虑以下 GDL 条目。

```cpp
*rcNameID:     ( RESDLL.stdname.467 )  
*rcNameID:      (0x117 )  
```

并考虑以下 RC\_名称\_ID2 模板。

```cpp
*Template:  RC_NAME_ID2
{
    *Name:  "*rcNameID"
    *Type:  ATTRIBUTE
    *ValueType:  INT_OR_QUALNAME_EX
    *Additive: LEAST_TO_MOST_RECENT
}
```

如果 GDL 条目进行解释由前面的模板，生成的 XML 输出将如下所示。

```cpp
<GDL_ATTRIBUTE Name="*rcNameID"  Personality="QualNameEx" >
   <feature  xsi:type="GDLW_string">RESDLL</feature>
   <option  xsi:type="GDLW_string">stdname</option>
   <resourceID  xsi:type="GDLW_int">467</resourceID>
</GDL_ATTRIBUTE>
<GDL_ATTRIBUTE Name="*rcNameID"  Personality="integer" 
xsi:type="GDLW_int" >279</GDL_ATTRIBUTE>
```

从多个生成的 XML 输出之间的唯一区别\_个性类型和实际类型是为了通知客户端的值的实际数据类型的其他个性标记属性。

例如，可以创建数组，其中数组的每个成员都倍数\_个性类型，按如下所示。

```cpp
*Template:  DT_ARRAY_OF_MP
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  INT_OR_QUALNAME_EX
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (ArrayMember)
    *ArraySize: *
}
*Template:  ARRAY_OF_MP
{
    *Name:  "*rcNameID_List"
    *Type:  ATTRIBUTE
    *ValueType:  DT_ARRAY_OF_MP
}
```

并使用前面的模板来处理以下实例数据，这是一个数组，包含三个多属性对象，其中每个恰好有不同的个性。

```cpp
*rcNameID_List:( RESDLL.stdname.467, 0x117, "Quote" )
```

此处理过程将生成以下 XML 快照。

```cpp
    <GDL_ATTRIBUTE Name="*rcNameID_List"  >
        <ArrayMember  Personality="QualNameEx">
            <feature  xsi:type="GDLW_string">RESDLL</feature>
            <option  xsi:type="GDLW_string">stdname</option>
            <resourceID  xsi:type="GDLW_int">467</resourceID>
        </ArrayMember>
        <ArrayMember  Personality="integer" xsi:type="GDLW_int">279</ArrayMember>
        <ArrayMember  Personality="QuotedString" xsi:type="GDLW_string">Quote</ArrayMember>
    </GDL_ATTRIBUTE>
```

如快照所示，分析器将为每个三个数组成员确定正确的个性，并将个性属性设置在每个成员的元素以指示相应的个性。

 

 




