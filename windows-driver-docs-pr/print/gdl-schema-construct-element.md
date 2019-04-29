---
title: GDL 架构构造元素
description: GDL 架构构造元素
ms.assetid: 46653504-4ce7-455c-a22a-a6032cbd6a3e
keywords:
- GDL WDK 元素
- GDL WDK 架构
- 构造元素 WDK GDL
- 快照 WDK GDL，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3328437244059dc780f95ceae244ffe0c9d53c3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366435"
---
# <a name="gdl-schema-construct-element"></a>GDL 架构构造元素


GDL 分析器生成的 XSD 架构定义的构造元素，如下所示：

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

前面的定义是类似的定义[ &lt;SnapshotRoot&gt;元素](gdl-schema-root-element.md)。 和构造类似的根元素的元素，可以容纳构造 (&lt;构造&gt;) 和属性 (&lt;GDL\_特性&gt;) 元素。 但是， &lt;GDL\_ConstructType&gt;可以有三个其他 XML 属性：**名称**，**实例**，和**约束**。 **名称**并**实例**和所需和分别保存名称和实例 GDL 构造。 **约束**是可选的包含一个布尔值，该值指示是否是否约束选项。 此属性仅出现&lt;构造&gt;对应的元素\*选项构造。

例如，考虑以下 GDL 条目。

```cpp
*Feature:  PaperSize
{
   *Option:  Letter
   {
   }
}
```

上一项会导致以下 XML 快照。

```cpp
     <CONSTRUCT Name="*Feature" Instance="PaperSize">
        <CONSTRUCT Name="*Option" Instance="Letter" Constrained="FALSE" >
        </CONSTRUCT>
    </CONSTRUCT>
```

特定选项标记为受约束，具体取决于提供的配置和 GDL 实例数据中定义的约束的设置。

 

 




