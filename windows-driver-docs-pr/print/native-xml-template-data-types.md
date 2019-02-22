---
title: 本机 XML 模板数据类型
description: 本机 XML 模板数据类型
ms.assetid: a34dec46-de5d-4f12-8863-2fe6b6e5eed4
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- 本机数据类型 WDK GDL
- XML_TYPE WDK GDL
- ArrayLabel 指令 WDK GDL
- XMLDataType 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 719d28be12cb3adaf19fccf2a28d192689855523
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543982"
---
# <a name="native-xml-template-data-types"></a>本机 XML 模板数据类型


本机 XML 数据类型定义为 XML\_类型。

语法定义的 XML。 可以定义识别的 XML 架构的任何数据类型。 因此，当前的分析器可以支持未来的 XML 数据类型，无需更改任何分析器筛选器不依赖于 XML 数据类型。

\***数据类型**:**XML\_类型**将模板与特定的 XML 架构定义语言的内置简单数据类型相关联。 实例数据值将作为 XML 元素的内容的输出**xsi: type**派生自\* **XMLDataType**构造，它指定此模板。

以下指令用于定义 XML\_数据类型：

-   \*XMLDataType （必需）。 任何 XSD 架构内置简单类型。 [World Wide Web 联合会 (W3C)](https://go.microsoft.com/fwlink/p/?linkid=73527)的 XML 架构建议可以识别以下内置的简单数据类型： string、 normalizedString、 令牌、 字节、 unsignedByte、 base64Binary、 hexBinary、 integer、positiveInteger、 negativeInteger、 nonNegativeInteger、 nonPositiveInteger，int，unsignedInt，长，unsignedLong，短、 无符号 Short、 decimal、 float、 double、 布尔值、 时间、 日期时间、 持续时间、 日期、 gMonth、 gYear、 gYearMonth、 gDay、 gMonthDay，名称，QName、 NCName、 anyURI、 语言、 ID、 IDREF、 IDREFS、 实体、 实体、 表示法、 NMTOKEN 和 NMTOKENS。 请注意 GDL 分析器并不局限于这些数据类型，它旨在处理将来的 XML 数据类型，无需进行任何更改。

-   \*ArrayLabel （可选）。 如果指定此指令时，分析器筛选器需要括在圆括号，以指定的数组标签值。

值的语法必须符合 W3C XML 标准定义为该特定的数据类型的语法。 如果与基本 GDL 语法规则冲突的 XML 语法的值 （或只是冲突的部分） 必须括起&lt;Begin/EndValue:&gt;构造。 XML 值与此类不兼容的语法，或其语法不兼容的语法由复合数据类型，不能显示为复合数据类型的成员。 此外请注意 GDL 分析器将不会转义特殊 XML 字符如打开或右括号 (&lt;或&gt;) 或与号 (&)。 值的创建者负责符合用于字符数据的 XML 语法。

例如，考虑以下模板。

```cpp
*Template:  XML_STRING
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "string"
}
```

如果使用前面的模板，将创建以下 XML 架构项。 此项定义派生自最初指定的类型的新数据类型\* **XMLDataType**指令，但在此新的数据类型具有可以在快照中显示的其他 XML 特性。 如果你使用的原始数据类型，则会收到架构验证错误，因为原始预定义的类型不允许出现 XML 特性。

```cpp
    <complexType name = "GDLW_string">
        <simpleContent>
            <extension base="string">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </simpleContent>
    </complexType>
```

请考虑以下 GDL 条目。

```cpp
*Text: Hello World
```

请考虑短语模板声明 GDL 属性\***文本**具有\* **ValueType**由 XML\_字符串作为模板，下面的代码示例显示了。

```cpp
*Template:  PHRASE
{
    *Name:  "*Text"
    *Type:  ATTRIBUTE
    *ValueType:  XML_STRING
}
```

如果早期 GDL 条目解释使用短语模板中，将发生以下 XML 输出。

```cpp
<GDL_ATTRIBUTE Name="*Text"  xsi:type="GDLW_string" >Hello World</GDL_ATTRIBUTE>
```

XML 特性**xsi: type**用来指定由于架构包含此元素没有声明，此属性元素保留的数据类型。

 

 




