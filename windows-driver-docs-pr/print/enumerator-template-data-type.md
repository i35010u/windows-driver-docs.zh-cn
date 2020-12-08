---
title: 枚举器模板数据类型
description: 枚举器模板数据类型
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- 枚举器数据类型 WDK GDL
- ArrayLabel 指令 WDK GDL
- XMLDataType 指令 WDK GDL
- EnumeratorList 指令 WDK GDL
- ElementTags 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3297fc9de1677e452a73dbfcf4168b41f4a3a3b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797121"
---
# <a name="enumerator-template-data-type"></a>枚举器模板数据类型


枚举器数据类型的允许值限制为一组标记。

\*DataType：枚举器定向模板来定义枚举数据类型。 此数据类型将作为 XML 架构 simpleType 声明输出，该声明派生自 **字符串** 类型，并且具有指定每个允许的枚举数的限制。 以下指令用于完全定义枚举器数据类型：

-   \*需要) XMLDataType (。 要分配给 XML 数据类型的 NCName，该数据类型将用于在生成的 XML 架构中定义此枚举。 每个枚举类型必须具有唯一的 NCName。 此名称对于所有 XSD \_ 定义的类型和枚举器类型必须是唯一的。 若要避免与 GDL 分析器定义的数据类型发生冲突，应避免 NCNames 以 "GDL \_ " 和 "GDLW" 开头 \_ 。

-   \*需要) EnumeratorList (。 枚举器标记的列表。 每个标记都必须是有效的 GDL 符号，并且必须符合 XSD 架构对架构组件：枚举的值施加的任何其他要求 &lt; &gt; 。

-   \*ArrayLabel (可选) 。 如果指定此指令，则分析器筛选器会将值括在括号内，并在其前面加上指定的数组标签。

要作为枚举器数据类型进行分析的值必须与 ElementTags 指令定义的标记之一匹配 \* 。

请考虑以下模板。

```cpp
*Template:  COLORS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "colors"
    *EnumeratorList: (YELLOW, MAGENTA, CYAN, BLACK, RED, GREEN, BLUE)
}
```

上述模板会导致分析器筛选器创建以下 XML 架构条目。

```cpp
    <simpleType name = "colors">
        <restriction base="string">
            <enumeration value="YELLOW"/>
            <enumeration value="MAGENTA"/>
            <enumeration value="CYAN"/>
            <enumeration value="BLACK"/>
            <enumeration value="RED"/>
            <enumeration value="GREEN"/>
            <enumeration value="BLUE"/>
        </restriction>
    </simpleType>
```

分析器筛选器还会创建相应的换行数据类型。

```cpp
    <complexType name = "GDLW_colors">
        <simpleContent>
            <extension base="gdl:colors">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </simpleContent>
    </complexType>
```

请考虑以下 GDL 条目。

```cpp
*Color: GREEN
```

并考虑 ACOLOR 模板，该模板将 **\* 颜色** GDL 属性声明为具有模板颜色定义的 **\* ValueType** ，如以下代码示例所示。

```cpp
*Template:  ACOLOR
{
    *Name:  "*Color"
    *Type:  ATTRIBUTE
    *ValueType:  COLORS
    *Additive: LEAST_TO_MOST_RECENT
}
```

如果使用 ACOLOR 模板解释前面的 GDL 项，则会生成 XML 输出。

```cpp
    <GDL_ATTRIBUTE Name="*Color"  xsi:type="GDLW_colors" >GREEN</GDL_ATTRIBUTE>
```

XML 属性 **xsi： type** 定义 GDL attribute 元素的此实例 \_ ，以保存模板定义的值类型，该类型表示在 XML 默认命名空间中定义的枚举。

 

 




