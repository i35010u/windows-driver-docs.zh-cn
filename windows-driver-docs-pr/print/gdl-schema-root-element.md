---
title: GDL 架构根元素
description: GDL 架构根元素
ms.assetid: 6148f026-52fa-452d-aa81-564d6ee5288d
keywords:
- GDL WDK 元素
- GDL WDK 架构
- SnapshotRoot 元素 WDK GDL
- 根元素 WDK GDL
- 快照 WDK GDL，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0064121920559af2d9dd36dd8acb1a2337fd66bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346611"
---
# <a name="gdl-schema-root-element"></a>GDL 架构根元素


GDL 分析器生成的 XSD 架构定义的根元素 (&lt;SnapshotRoot&gt;)，如下所示：

```cpp
    <element name="SnapshotRoot" type="gdl:GDL_RootType"/>

    <complexType name="GDL_RootType"  >
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
    </complexType>
```

XSD 架构不允许&lt;任何&gt;元素与共存定义元素类型，因此分析器的架构会保留其定义的根元素非常灵活。 尽管 XSD 架构故意留非常一般&lt;SnapshotRoot&gt;元素可以包含任意数量的&lt;GDL\_特性&gt;或&lt;构造&gt;按任意顺序的元素。 由于最新定义条目 GDL 语言的强调，XML 快照中的元素的外观通常与 GDL 源文件中的项的外观的相反。

&lt;SnapshotRoot&gt;元素是快照文档中的最外层元素，它包含所有快照中的其他元素。 只有一个&lt;SnapshotRoot&gt;每个快照中的元素。

 

 




