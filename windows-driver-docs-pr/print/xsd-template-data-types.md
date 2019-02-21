---
title: XSD 模板数据类型
description: XSD 模板数据类型
ms.assetid: 96d3a75a-fa15-47bb-8331-e3994d25c42d
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- XSD_DEFINED 数据类型 WDK GDL
- ArrayLabel 指令 WDK GDL
- XMLDataType 指令 WDK GDL
- XSDTypeDefinition 指令 WDK GDL
- ComplexType 指令 WDK GDL
- 分析器 WDK GDL，转义特殊 XML 字符
- 转义特殊 XML 字符 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be818179c0e27790b0b453a256355400933ae891
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541281"
---
# <a name="xsd-template-data-types"></a>XSD 模板数据类型


XSD\_定义数据类型使用的数据类型的定义架构。 您可以定义任何复杂类型或简单类型。

\*数据类型：XSD\_定义创建的数据类型定义通过使用标准&lt;xsd: complextype&gt;或&lt;xsd: simpletype&gt; XML 元素。 实例数据值作为其 xsi: type 指定的值的 XML 元素的内容将输出\*XMLDataType 出现在此模板中。 此输出，可使用 XSD 派生新的简单或复杂类型并将其用于 GDL 属性。

以下指令用于完全定义 XSD\_定义数据类型：

-   \*XMLDataType （必需）。 已分配给此模板定义的 XSD 数据类型的名称 (NCName)。 此名称为的值**名称**属性中&lt;complexType&gt;或&lt;simpleType&gt;元素的\*XSDTypeDefinition 指令定义。 此名称必须是唯一的所有 XSD\_定义和枚举器类型。 若要避免冲突 GDL 分析器定义的数据类型，应避免开头的名称"GDL\_"和"GDLW\_"。 XML 标准定义的 NCName 的语法，并可能有附加限制。

-   \*XSDTypeDefinition （必需）。 格式正确的 XSD 定义的数据类型。 仅&lt;complexType&gt;或&lt;simpleType&gt;元素可以出现在离根最近的上下文。 多个&lt;complexType&gt;或&lt;simpleType&gt;如果最多仅有一种实际引用为 GDL 属性的值类型元素可能会显示为在最根本的上下文的同级。 因为 GDL 属性的值类型是中显示的引用的类型名称\*XMLDataType 指令。 剩余的数据类型只能从中其他引用&lt;complexType&gt;或&lt;simpleType&gt;定义。

    类型定义还可以引用其他模板中定义其他类型定义。 当引用类型定义内的\*XSDTypeDefinition 指令创建的使用\*XSDTypeDefinition 指令，则必须使用 gdl： 命名空间前缀。

    如果 XSD 占用多行，或者如果它违反了 GDL 语法规则，则必须用通过&lt;Begin/EndValue&gt;分隔符。 在此分隔符中定义的 XSD 将插入到 GDL 分析器生成的 XSD 架构。 请注意， &lt;complexType&gt;如 GDL 属性的值类型不能声明任何 XML 特性将引用的定义。 在 GDL 分析器生成的架构，XSD 命名空间是默认命名空间，因此元素名称等&lt;complexType&gt;或&lt;序列&gt;或&lt;元素&gt;不需要命名空间限定符。 目标命名空间是与 gdl 相关联： 前缀。

-   \*复杂类型？ (**，则返回 TRUE** | **FALSE**) （可选）。 如果此指令很 **，则返回 TRUE**，GDL 分析器将引用此定义作为&lt;complexContent&gt;时扩展此数据类型; 否则，定义被引用为&lt;simpleContent&gt;. 如果未指定此指令，分析器将假定它是**FALSE**。

-   \*ArrayLabel （可选）。 如果指定此指令，则分析器筛选器应括在圆括号，以指定的数组标签此类型的实例值。

被声明为此数据类型的值实例的语法必须遵守由 XSD 定义的语法的\*XSDTypeDefinition 指令提供。 分析器将提供开始和结束元素标记和值实例数据应提供仅元素内容。 如果与基本 GDL 语法规则冲突的 XML 语法的值 （或只是冲突的部分） 必须括起&lt;Begin/EndValue:&gt;构造。

XML 值与此类不兼容的语法，或其语法与不兼容的语法的复合数据类型使用，不能显示为复合数据类型的成员。 此外请注意 GDL 分析器将不会转义特殊 XML 字符如打开或右括号 (&lt;或&gt;) 或与号 (&)。 值实例的创建者负责符合用于字符数据的 XML 语法。

例如，考虑以下模板。

```cpp
*Template:  USAddress
{
    *Type:  DATATYPE
    *DataType:   XSD_DEFINED
    *ComplexType?: TRUE
    *XMLDataType: "USAddress"
    *XSDTypeDefinition:<BeginValue:XSD>
    <complexType name="USAddress">
        <sequence>
            <element name="name"   type="string"/>
            <element name="street" type="string"/>
            <element name="city"   type="string"/>
            <element name="state"  type="string"/>
            <element name="zip"    type="gdl:zipCode"/>
        </sequence>
    </complexType>

<simpleType name="zipCode">
 <restriction base="integer">
  <minInclusive value="10000"/>
  <maxInclusive value="99999"/>
 </restriction>
</simpleType><EndValue:XSD>
}
```

前面的示例定义名为"USAddress"可通过为其 ValueType GDL 属性引用的 XSD 定义的类型。 此 XSD 示例实际上定义了两种数据类型：**USAddress**并**zipCode**。 **ZipCode**类型不能引用由 GDL 属性和可以仅从另一个 XSD 数据类型定义中引用。

在以下示例中， **zipCode**中的声明引用类型&lt;zip&gt;元素。 请注意，它引用通过使用 gdl： 命名空间前缀。 **zipCode**还可以从另一个模板中的 XSD 数据类型定义中引用。

前面的模板定义将导致以下 XML 架构条目的创建 (它是值的\*XSDTypeDefinition 保持不变)。

```cpp
    <complexType name="USAddress">
        <sequence>
            <element name="name"   type="string"/>
            <element name="street" type="string"/>
            <element name="city"   type="string"/>
            <element name="state"  type="string"/>
            <element name="zip"    type="gdl:zipCode"/>
        </sequence>
    </complexType>

    <simpleType name="zipCode">
        <restriction base="integer">
            <minInclusive value="10000"/>
            <maxInclusive value="99999"/>
        </restriction>
    </simpleType>
```

分析器自动构造定义一个派生自的新类型的另一种数据类型**USAddress**类型，但这有可能会出现在快照中的其他 XML 属性。 如果使用原始数据类型，则会收到架构验证错误，因为对于任何 XML 特性出现不允许使用原始类型。 使用此方法时，你未安装到在模板中硬编码分析器合成 XML 特性和其他属性添加到快照的未来版本中，如果您不需要修改现有模板。

下面的代码示例显示了其他数据类型定义。

```cpp
    <complexType name = "GDLW_USAddress">
        <complexContent>
            <extension base="gdl:USAddress">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </complexContent>
    </complexType>
```

**请注意**   **GDLW\_USAddress**数据类型被声明为&lt;complexContent&gt;因为的模板**USAddress**设置\*ComplexType？:**TRUE**。

 

请考虑以下 GDL 条目。

```cpp
*Address: <BeginValue:XML> 
   <name>Alice Smith</name>
   <street>123 Maple Street</street>
   <city>Mill Valley</city>
   <state>CA</state>
   <zip>90952</zip>
<EndValue:XML>
```

并考虑地址模板，用于声明\*地址 GDL aAttribute 能够\*由模板定义的 ValueType **USAddress**，如下面的代码示例所示。

```cpp
*Template:  ADDRESS
{
    *Name: "*Address"
    *Type:  ATTRIBUTE
    *ValueType:  USAddress
}
```

如果早期 GDL 条目被解释使用地址模板，生成的 XML 输出会发生。

```cpp
    <GDL_ATTRIBUTE Name="*Address"  xsi:type="GDLW_USAddress" >
    <name>Ben Smith</name>
    <street>123 Maple Street</street>
    <city>Mill Valley</city>
    <state>CA</state>
    <zip>90952</zip>
    </GDL_ATTRIBUTE>
```

XML 属性 xsi: type 定义要包含名为 XSD 定义的数据类型的属性元素的此实例**GDLW\_USAddress**。 GDL 特性实例的整个值插入到的元素内容作为&lt;GDL\_属性&gt;无需任何修改 XML 快照中的元素。 因此，值必须是有效的 XML，并且必须遵循所有 XML 语法规则，等特殊字符的表示形式。

 

 




