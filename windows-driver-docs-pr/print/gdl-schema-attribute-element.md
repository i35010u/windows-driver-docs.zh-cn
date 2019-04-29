---
title: GDL 架构属性元素
description: GDL 架构属性元素
ms.assetid: b46c0c6c-28af-4121-9182-65dc23b0ce7d
keywords:
- GDL WDK 元素
- GDL WDK 架构
- attribute 元素 WDK GDL
- GDL_ATTRIBUTE WDK GDL
- GDL_UntypedAtt WDK GDL
- 非类型化的属性 WDK GDL
- 快照 WDK GDL，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff08d7b1f570dc8f52d67260c996251feeac2f71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380167"
---
# <a name="gdl-schema-attribute-element"></a>GDL 架构属性元素


所有的数据类型&lt;GDL\_特性&gt;根据每个实例使用指定元素**xsi: type**。 属性没有特定的数据类型定义指定的泛型属性元素的实例 (&lt;GDL\_UntypedAtt&gt;)，这是在架构中定义 GDL 生成，如下所示：

```cpp
    <complexType name="GDL_UntypedAtt"  mixed="true">
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
        <attribute name="Name" type="string" use="required"/>
        <attribute name="Personality" type="string" use="optional"/>
    </complexType>
```

更具体的数据类型不所描述的属性的内容时使用此泛型数据类型。 通用的数据类型不限制可以出现的元素内容。 由 GDL 数据类型模板确定实际元素内容。

&lt;GDL\_UntypedAtt&gt;有两个属性：**名称**并**个性**。 **名称**是必需的包含 GDL 属性的关键字名称。 **个性**是可选的如果该属性定义为指定的个性标记\*数据类型：多个\_个性。

如果 GDL 数据类型的值的专门定义 XSD 架构中，通过引用定义的数据类型**xsi: type**属性。 XML\_类型、 枚举和 XSD\_定义数据类型在 XSD 架构中创建新的数据类型。

GDL 复合数据类型由泛型数据类型表示。 复合数据类型的实例包含可能包含其他子元素的子元素或表示简单的 XML 数据类型的字符内容。 由定义的子元素的名称 **\*ElementTags**指令的数据类型模板。

没有定义的数据类型或不是与模板关联或不符合指定的数据类型的预期的语法的 GDL 属性的值由&lt;CDATA&gt;主题中&lt;GDL\_属性&gt;元素。 此部分中，客户端或其他分析器筛选器来处理他们所需的值。 此类未知的数据类型将不包含**xsi: type**属性。 多个&lt;CDATA&gt;可能会要求部分表示的值，如果值包含字符串"\]\]&gt;"。

 

 




