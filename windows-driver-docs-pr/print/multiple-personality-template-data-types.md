---
title: 多个个性化模板数据类型
description: 多个个性化模板数据类型
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，复合
- MULTIPLE_PERSONALITY 数据类型 WDK GDL
- ElementType 指令 WDK GDL
- ElementTags 指令 WDK GDL
- 联合 WDK GDL
- GDL WDK，联合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e4bc81880f8ee734386abafabce2fc403c71b97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807835"
---
# <a name="multiple-personality-template-data-types"></a>多个个性化模板数据类型


多项 \_ 个性数据类型表示可以在不同时间容纳不同数据类型的值。 此数据类型类似于 C 语言 **联合** 数据类型。

\*数据类型：多项 \_ 个性指导模板定义一个数据类型，该数据类型可以接受属于多个不同数据类型的值，这与 C 语言 **联合** 数据类型非常相似。 多项 \_ 个性数据类型试图确定标识 (即值的数据类型) ，并输出相同的 XML，就好像在模板中显式定义了该值，使其属于标识的数据类型一样。 换言之，如果定义了多项 \_ 个性数据类型来保存字符串或整数或符号，并且该值实际包含整数，则 XML 输出将为 integer 数据类型。

还发出了一个个性标记属性，以帮助客户端确定所发出的值的数据类型。 筛选器通过使用每个可能的数据类型来分析值，从而确定值的数据类型。 将选择成功匹配输入值的最大数量的数据类型。 发生关联时，将选择列表中第一个出现的元素类型。

**注意**   您可以构造可引诱此计算算法的值语法，因此在选择要列出的元素类型时请小心。 这些类型必须可通过分析算法充分区分。 例如，由于分析器筛选器不能识别任何 XML 语法，因此它不能区分两个 XML \_ 类型数据类型。 但是，在这种情况下，候选数据类型的定义可以包含 \* ArrayLabel 指令，这将帮助分析器区分它们。

 

以下指令用于定义多项 \_ 个性数据类型：

-   \*ElementType (必需的) 。 模板名称的列表，用于定义此值可采用的可能的数据类型。

-   \*需要) ElementTags (。 用于帮助客户端标识实际分配给该值的数据类型的标记列表。 提供的标记数应该等于 ElementType 中列出的模板数 \* 。 标记将显示在生成的 XML 元素（表示值）的 "个性" 属性中。 例如，如果数据类型是多个特性数据类型的数组，则表示该数组的各个成员的元素将包含个性特性。 表示整个数组的元素不会包含个性特性，因为数组本身不具有定义的个性。相反，数组的各个成员具有其各自不同的个性特性值。

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

此模板定义一个数据类型，该数据类型可以保存整数值、QUALNAME \_ EX 值或 QUOTEDSTRING 值。 选择的任何数据类型都将用相应的用户定义的 ElementTag 标识。

请考虑以下 GDL 条目。

```cpp
*rcNameID:     ( RESDLL.stdname.467 )  
*rcNameID:      (0x117 )  
```

并考虑以下 RC \_ NAME \_ ID2 模板。

```cpp
*Template:  RC_NAME_ID2
{
    *Name:  "*rcNameID"
    *Type:  ATTRIBUTE
    *ValueType:  INT_OR_QUALNAME_EX
    *Additive: LEAST_TO_MOST_RECENT
}
```

如果前面的模板解释了 GDL 项，则生成的 XML 输出将如下所示。

```cpp
<GDL_ATTRIBUTE Name="*rcNameID"  Personality="QualNameEx" >
   <feature  xsi:type="GDLW_string">RESDLL</feature>
   <option  xsi:type="GDLW_string">stdname</option>
   <resourceID  xsi:type="GDLW_int">467</resourceID>
</GDL_ATTRIBUTE>
<GDL_ATTRIBUTE Name="*rcNameID"  Personality="integer" 
xsi:type="GDLW_int" >279</GDL_ATTRIBUTE>
```

从多项 "类型" 和 "实际类型" 生成的 XML 输出的唯一区别 \_ 是附加的 "个性" 标记属性，添加该属性是为了通知客户端值的实际数据类型。

例如，可以创建一个数组，其中数组的每个成员都是多项 \_ 个性类型，如下所示。

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

您可以使用前面的模板来处理以下实例数据，这是一个包含三个多项个性对象的数组，其中每个对象都有不同的个性。

```cpp
*rcNameID_List:( RESDLL.stdname.467, 0x117, "Quote" )
```

此处理将生成以下 XML 快照。

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

如快照所示，分析器为三个数组成员的每个成员确定了正确的个性，并在每个成员的元素中设置了 "个性" 属性以指示适当的个性。

 

 




