---
title: GDL 架构属性元素
description: GDL 架构属性元素
keywords:
- GDL WDK，元素
- GDL WDK，架构
- attribute 元素 WDK GDL
- GDL_ATTRIBUTE WDK GDL
- GDL_UntypedAtt WDK GDL
- 非类型化属性 WDK GDL
- 快照 WDK GDL，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae035114679f6198b5d999db9ccc80ec77f8b82c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835923"
---
# <a name="gdl-schema-attribute-element"></a>GDL 架构属性元素


所有 &lt; GDL 属性元素的数据 \_ 类型 &gt; 都是使用 **xsi： type** 基于每个实例指定的。 没有特定数据类型定义的属性是泛型 attribute 元素的指定实例 (&lt; GDL \_ UntypedAtt &gt;) ，它在 GDL 生成的架构中定义，如下所示：

```cpp
    <complexType name="GDL_UntypedAtt"  mixed="true">
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
        <attribute name="Name" type="string" use="required"/>
        <attribute name="Personality" type="string" use="optional"/>
    </complexType>
```

当特性的内容未由更具体的数据类型描述时，将使用此泛型数据类型。 泛型数据类型不限制可显示的元素内容。 实际元素内容由 GDL 数据类型模板决定。

&lt;GDL \_ UntypedAtt &gt; 有两个属性： **Name** 和 **个性**。 **名称** 是必需的，并保存 GDL 属性的关键字名称。 "**个性**" 是可选的，如果属性定义为 DataType，则指定 "个性" 标记 \* ：多项 \_ 个性。

如果值的 GDL 数据类型是在 XSD 架构中明确定义的，则该定义的数据类型由 **xsi： type** 特性引用。 XML \_ 类型、枚举器和 xsd \_ 定义的数据类型在 XSD 架构中创建新的数据类型。

GDL 复合数据类型由泛型数据类型表示。 复合数据类型的实例包含可能包含其他子元素的子元素或表示简单 XML 数据类型的字符内容。 子元素的名称由 DATATYPE 模板的 **\* ElementTags** 指令定义。

如果 GDL 属性的值没有定义的数据类型，或者未与模板关联，或者不符合指定数据类型所需的语法，则 &lt; &gt; 在 &lt; GDL \_ ATTRIBUTE 元素中由 CDATA 节表示 &gt; 。 此部分使客户端或其他 Parser-Filters 可以根据需要处理该值。 这种未知数据类型将不包含 **xsi： type** 属性。 &lt; &gt; 如果值包含字符串 ""，则可能需要多个 CDATA 节来表示值 \] \] &gt; 。

 

 




