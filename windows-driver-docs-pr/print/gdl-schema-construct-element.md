---
title: GDL 架构构造元素
description: GDL 架构构造元素
keywords:
- GDL WDK，元素
- GDL WDK，架构
- 构造元素 WDK GDL
- 快照 WDK GDL，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e095e0d32f181ee8b551c7439afb6a3a89c93d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796953"
---
# <a name="gdl-schema-construct-element"></a>GDL 架构构造元素


GDL 分析器生成的 XSD 架构定义构造元素，如下所示：

```cpp
    <complexType name="GDL_ConstructType">
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
        <attribute name="Name" type="string" use="required"/>
        <attribute name="Instance" type="string" use="required"/>
        <attribute name="Constrained" type="boolean" use="optional"/>
    </complexType>
```

上述定义类似于[ &lt; SnapshotRoot &gt; 元素](gdl-schema-root-element.md)的定义。 构造元素与根元素一样，可以将构造 (&lt; 构造 &gt;) 和属性 (&lt; GDL \_ 特性 &gt;) 元素。 但是， &lt; GDL \_ ConstructType &gt; 可以有三个附加的 XML 属性： **名称**、 **实例** 和 **约束**。 **名称** 和 **实例** ，并分别保留名称和实例 GDL 结构。 "**约束**" 是可选的，并且包含一个布尔值，该值指示选项是否受限制。 此属性仅针对 &lt; 对应于 &gt; 选项构造的构造元素出现 \* 。

例如，请看下面的 GDL 项。

```cpp
*Feature:  PaperSize
{
   *Option:  Letter
   {
   }
}
```

上述条目将生成以下 XML 快照。

```cpp
     <CONSTRUCT Name="*Feature" Instance="PaperSize">
        <CONSTRUCT Name="*Option" Instance="Letter" Constrained="FALSE" >
        </CONSTRUCT>
    </CONSTRUCT>
```

根据提供的配置和在 GDL 实例数据中定义的约束集，特定选项被标记为 "已约束"。

 

 




