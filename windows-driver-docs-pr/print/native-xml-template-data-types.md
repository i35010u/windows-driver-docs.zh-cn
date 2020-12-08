---
title: 本机 XML 模板数据类型
description: 本机 XML 模板数据类型
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- 本机数据类型 WDK GDL
- XML_TYPE WDK GDL
- ArrayLabel 指令 WDK GDL
- XMLDataType 指令 WDK GDL
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 77c866e52c55732cc8884151a4dd2ccfb92fb50e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807811"
---
# <a name="native-xml-template-data-types"></a>本机 XML 模板数据类型

本机 XML 数据类型定义为 XML \_ 类型。

语法由 XML 定义。 可以定义 XML 架构可识别的任何数据类型。 分析器筛选器不依赖于 XML 数据类型，因此，当前分析器可以在不进行任何更改的情况下支持未来的 XML 数据类型。

\***DataType**： **XML \_ 类型** 将模板与特定 XML 架构定义语言的内置简单数据类型相关联。 实例数据值将作为 XML 元素的内容输出，其 **xsi： type** 派生自 \* 此模板指定的 *_XMLDataType_* 构造。

以下指令用于定义 XML \_ 类型数据类型：

- \*需要) XMLDataType (。 任何 XSD 架构内置简单类型。 XML 架构的 [万维网联合会 (W3C) ](https://www.w3.org/XML/Schema#dev) 建议识别以下内置简单数据类型： String、normalizedString、token、Byte、UnsignedByte、Base64Binary、hexBinary、Integer、PositiveInteger、NegativeInteger、NonNegativeInteger、nonPositiveInteger、Int、unsignedInt、Long、unsignedLong、Short、unsignedShort、decimal、float、double、boolean、Time、dateTime、duration、Date、GMonth、GYear、GYearMonth、GDay、GMonthDay、Name、QName、 请注意，GDL 分析器并不限于这些数据类型，设计用于处理将来的 XML 数据类型，而不进行任何更改。

- \*ArrayLabel (可选) 。 如果指定此指令，则分析器筛选器会将值括在括号内，并在其前面加上指定的数组标签。

值的语法必须符合 W3C XML 标准为该特定数据类型定义的语法。 如果 XML 语法与基本 GDL 语法规则冲突，则值 (或仅) 冲突部分必须包含在 <Begin/EndValue： > 构造内。 不兼容语法的 XML 值或其语法与复合数据类型所用语法不兼容的 XML 值不能作为复合数据类型的成员出现。 另请注意，GDL 分析器不会转义特殊的 XML 字符（如左括号或右括号） ( # A0 或 >) 或 ( # A2) 的与号。 值的创建者负责使字符数据符合 XML 语法。

例如，请考虑以下模板。

```console
*Template:  XML_STRING
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "string"
}
```

如果使用前面的模板，则将创建以下 XML 架构条目。 此项定义了从 XMLDataType 指令最初指定的类型派生的新数据类型 \* **XMLDataType** ，但此新数据类型具有可在快照中显示的其他 XML 属性。 如果使用的是原始数据类型，则会出现架构验证错误，因为原始预定义类型不允许显示 XML 属性。

```xml
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

```console
*Text: Hello World
```

请考虑短语模板，该模板将 GDL 特性 \* **文本** 声明为具有 \* *_ValueType_* 由 XML 字符串模板定义的 ValueType \_ ，如以下代码示例所示。

```console
*Template:  PHRASE
{
    *Name:  "*Text"
    *Type:  ATTRIBUTE
    *ValueType:  XML_STRING
}
```

如果使用短语模板解释前面的 GDL 项，则将发生以下 XML 输出。

```xml
<GDL_ATTRIBUTE Name="*Text"  xsi:type="GDLW_string" >Hello World</GDL_ATTRIBUTE>
```

XML 特性 **xsi： type** 用于指定此 attribute 元素保存的数据类型，因为架构不包含此元素的声明。
