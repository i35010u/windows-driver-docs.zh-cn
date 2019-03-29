---
title: 直通模板数据类型
description: 直通模板数据类型
ms.assetid: 9e5e6a12-5847-45fe-bee5-68944cd546d7
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- 传递数据类型 WDK GDL
- 架构 WDK GDL，验证传递的数据类型
- ArrayLabel 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 603633367691a26812f00800d17d7960169feb05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563103"
---
# <a name="passthrough-template-data-types"></a>直通模板数据类型


\***数据类型**:**传递**定义了一个模板来表示未处理的数据类型。 构成 GDL 值的字符作为元素内容的 XML 元素表示 GDL 属性插入。

在定义传递数据类型的模板中识别以下指令：

-   \*ArrayLabel。 如果指定此指令，则分析器筛选器需要要用括号括起来的值，并且前面加上指定的数组标签。 此指令是可选的。

值的语法必须遵守的可以包含字符数据、 子元素等 XML 元素内容定义的语法。 此外请注意 GDL 分析器将不会转义特殊 XML 字符的左或右括号等 (&lt;或&gt;) 或与号 (&)。 值的创建者负责符合元素内容的 XML 语法的值。

如果 XML 语法与基本 GDL 语法规则冲突，整个值 （或只是冲突的部分） 必须括起&lt;Begin/EndValue:&gt;构造。 XML 值与此类不兼容的语法，或其语法不兼容的语法由复合数据类型，不能显示为复合数据类型的成员，但必须显示直接为 GDL 属性的值。

例如，考虑下面的示例模板。

```cpp
*Template:  ELEMENT_CONTENT
{
    *Type:  DATATYPE
    *DataType:   PASSTHROUGH
}
```

与前面的模板，分析器筛选器不会创建传递数据的 XSD 架构数据类型声明。

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

如果上一项解释使用前面的示例模板，会发生以下 XML 输出。

```cpp
<GDL_ATTRIBUTE Name="*InLineXML"  >
  <Cell CellOrdinal="0">
    <Value xsi:type="xsd:double">16890</Value>
    <FmtValue>16,890.00</FmtValue>
    <FormatString>Standard</FormatString>
  </Cell>
</GDL_ATTRIBUTE>
```

如果你想要使用 XML 架构验证传递实例，则应使用[XSD\_定义数据类型](xsd-template-data-types.md)而不是传递，因为 XSD\_定义数据类型允许要进行的 XSD 架构显式模板中定义并由分析器集成到架构的输出。

 

 




