---
title: XSD 模板数据类型
description: XSD 模板数据类型
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
ms.openlocfilehash: eab1b4d145ce36530040d5a68949551e436fcf87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785685"
---
# <a name="xsd-template-data-types"></a>XSD 模板数据类型


XSD \_ 定义的数据类型使用架构作为数据类型的定义。 可以定义任意 ComplexType 或 SimpleType。

\*DataType： \_ 通过使用标准 &lt; Xsd： complexType &gt; 或 &lt; xsd： simpleType &gt; XML 元素，已定义 xsd 创建数据类型定义。 实例数据值将作为 XML 元素的内容输出，其 xsi： type 由 \* 此模板中显示的 XMLDataType 的值指定。 此输出使你可以使用 XSD 来派生新的简单类型或复杂类型，并在 GDL 属性中使用它们。

以下指令用于完全定义 XSD \_ 定义的数据类型：

-   \*需要) XMLDataType (。 已分配给此模板所定义的 XSD 数据类型 (NCName) 的名称。 此名称是 **name** &lt; &gt; &lt; &gt; \* XSDTypeDefinition 指令定义的 complexType 或 simpleType 元素中的 name 属性的值。 此名称对于所有 XSD \_ 定义的类型和枚举器类型必须是唯一的。 若要避免与 GDL 分析器定义的数据类型发生冲突，应避免名称以 "GDL \_ " 和 "GDLW" 开头 \_ 。 XML 标准定义 NCName 的语法，可能会施加其他限制。

-   \*需要) XSDTypeDefinition (。 定义数据类型的格式正确的 XSD。 只有 &lt; complexType &gt; 或 &lt; simpleType &gt; 元素可以出现在最靠近根的上下文中。 如果多个 &lt; complexType &gt; 或 &lt; simpleType 元素最多只能作为 GDL 属性的值类型进行引用，则多个 complexType 或 simpleType &gt; 元素可以在最根本的上下文中作为同级元素出现。 作为 GDL 属性的值类型引用的类型名称是出现在 XMLDataType 指令中的类型的名称 \* 。 其余数据类型只能从其他 &lt; complexType &gt; 或 &lt; simpleType 定义中引用 &gt; 。

    类型定义还可以引用其他模板中定义的其他类型定义。 引用 \* 使用 XSDTypeDefinition 指令创建的 XSDTypeDefinition 指令中的类型定义时 \* ，必须使用 gdl： namespace 前缀。

    如果 XSD 占用多行或违反 GDL 语法规则，则必须用 &lt; Begin/EndValue 分隔符括起来 &gt; 。 在此分隔符中定义的 XSD 将插入 GDL 分析器生成的 XSD 架构。 请注意， &lt; &gt; 将作为 GDL 属性的 ValueType 引用的 complexType 定义不能声明任何 XML 特性。 在 GDL 分析器生成的架构中，XSD 命名空间为默认命名空间，因此，元素名称（如 &lt; complexType &gt; 或 &lt; 序列 &gt; 或元素） &lt; &gt; 不需要命名空间限定符。 目标命名空间与 gdl： prefix 关联。

-   \*复杂?  (**TRUE**  |  **FALSE**)  (可选) 。 如果此指令为 **TRUE**，则在扩展此数据类型时，GDL 分析器会将此定义作为 &lt; complexContent 引用 &gt; ; 否则，定义将作为 &lt; simpleContent 引用 &gt; 。 如果未指定此指令，分析器将假定它为 **FALSE**。

-   \*ArrayLabel (可选) 。 如果指定此指令，则分析器筛选器需要将此类型的实例值括在括号内，并在其前面加上指定的数组标签。

声明为此数据类型的值实例的语法必须遵循 XSDTypeDefinition 指令提供的 XSD 所定义的语法 \* 。 分析器将为元素提供开始标记和结束标记，值实例数据应仅提供元素内容。 如果 XML 语法与基本 GDL 语法规则冲突，则值 (或只包含冲突部分) 必须在 &lt; Begin/EndValue：构造内包含 &gt; 。

具有这种不兼容语法的 XML 值或其语法与复合数据类型使用的语法不兼容，不能作为复合数据类型的成员出现。 另请注意，GDL 分析器将不会转义特殊的 XML 字符（如左括号或右括号） (&lt; 或 &gt;) 或 ( # A0) 。 值实例的创建者负责使字符数据符合 XML 语法。

例如，请考虑以下模板。

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

前面的示例定义了一个名为 "USAddress" 的 XSD 定义的类型，该类型可由 GDL 属性引用为其 ValueType。 此 XSD 示例实际定义两种数据类型： **USAddress** 和 **zipCode**。 **ZipCode** 类型不能由 GDL 特性引用，并且只能从另一个 XSD 数据类型定义中引用。

在下面的示例中， **zipCode** 在 zip 元素的声明中引用了 zipCode &lt; 类型 &gt; 。 请注意，使用 gdl： namespace 前缀引用它。 还可以从另一个模板中的 XSD 数据类型定义引用 **zipCode** 。

前面的模板定义将导致创建以下 XML 架构条目， (它是 XSDTypeDefinition 的值 \* 不更改) 。

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

分析器会自动构造另一种数据类型，该数据类型定义了从 **USAddress** 类型派生的新类型，但该类型具有可能出现在快照中的其他 XML 属性。 如果使用原始数据类型，则会出现架构验证错误，因为原始类型不允许显示任何 XML 特性。 使用此方法时，你无需在模板中硬编码分析器合成的 XML 特性，如果将其他特性添加到快照的未来版本中，则无需修改现有模板。

下面的代码示例演示了其他数据类型定义。

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

**注意**  **GDLW \_ USAddress** 数据类型被声明为 &lt; complexContent &gt; ，因为 **USAddress** set ComplexType 的模板为 \* **TRUE**。

 

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

并考虑地址模板，它将 \* 地址 GDL aAttribute 声明为具有 \* 模板 **USAddress** 定义的 ValueType，如以下代码示例所示。

```cpp
*Template:  ADDRESS
{
    *Name: "*Address"
    *Type:  ATTRIBUTE
    *ValueType:  USAddress
}
```

如果使用 ADDRESS 模板解释前面的 GDL 项，则会生成 XML 输出。

```cpp
    <GDL_ATTRIBUTE Name="*Address"  xsi:type="GDLW_USAddress" >
    <name>Ben Smith</name>
    <street>123 Maple Street</street>
    <city>Mill Valley</city>
    <state>CA</state>
    <zip>90952</zip>
    </GDL_ATTRIBUTE>
```

XML 属性 xsi： type 定义 ATTRIBUTE 元素的此实例，以保存名为 " **GDLW \_ USAddress**" 的 XSD 定义数据类型。 GDL 特性实例的整个值作为元素内容插入到 &lt; \_ XML 快照的 GDL attribute &gt; 元素中，无需进行任何修改。 因此，该值必须是有效的 XML，并且必须遵循所有 XML 语法规则，如特殊字符的表示形式。

 

 




