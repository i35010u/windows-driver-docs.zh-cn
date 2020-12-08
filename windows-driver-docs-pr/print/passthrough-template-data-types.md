---
title: 直通模板数据类型
description: 直通模板数据类型
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- 传递数据类型 WDK GDL
- 架构 WDK GDL，验证 PASSTHROUGH 数据类型
- ArrayLabel 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57e9e068807dcae8f08f7240fcd417fd37a8f316
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807631"
---
# <a name="passthrough-template-data-types"></a>直通模板数据类型


\***DataType**： **PASSTHROUGH** 定义用于表示未处理的数据类型的模板。 构成 GDL 值的字符作为 XML 元素的元素内容插入，表示 GDL 属性。

以下指令在定义 PASSTHROUGH 数据类型的模板中被识别：

-   \*ArrayLabel. 如果指定了此指令，则分析器筛选器会将值括在括号内，并将其放在指定的数组标签之前。 此指令是可选的。

值的语法必须遵循为 XML 元素内容定义的语法，该语法可包含字符数据、子元素等。 另请注意，GDL 分析器不会转义特殊的 XML 字符（如左括号或右括号） (&lt; 或 &gt;) 或 ( # A0) 。 值的创建者负责将值与元素内容的 XML 语法进行一致。

如果 XML 语法与基本 GDL 语法规则冲突，则整个值 (或只包含冲突部分) 必须在 &lt; Begin/EndValue：构造内包含 &gt; 。 具有这种不兼容语法的 XML 值或其语法与复合数据类型使用的语法不兼容，不能作为复合数据类型的成员显示，但必须直接显示为 GDL 属性的值。

例如，请看下面的示例模板。

```cpp
*Template:  ELEMENT_CONTENT
{
    *Type:  DATATYPE
    *DataType:   PASSTHROUGH
}
```

使用上述模板，分析器筛选器不会为传递数据创建 XSD 架构数据类型声明。

请考虑以下 GDL 条目。

```cpp
*InLineXML:  <BeginValue:XML>
 <Cell CellOrdinal="0">
         <Value xsi:type="xsd:double">16890</Value>
         <FmtValue>16,890.00</FmtValue>
         <FormatString>Standard</FormatString>
      </Cell>
<EndValue:XML>
```

如果使用前面的示例模板解释前面的条目，则将发生以下 XML 输出。

```cpp
<GDL_ATTRIBUTE Name="*InLineXML"  >
  <Cell CellOrdinal="0">
    <Value xsi:type="xsd:double">16890</Value>
    <FmtValue>16,890.00</FmtValue>
    <FormatString>Standard</FormatString>
  </Cell>
</GDL_ATTRIBUTE>
```

如果要使用 XML 架构验证传递实例，则应使用 [xsd \_ 定义的数据类型](xsd-template-data-types.md) 而不是 PASSTHROUGH，因为 xsd \_ 定义的数据类型允许在模板中显式定义 xsd 架构，并将其集成到分析器的架构输出中。

 

 




