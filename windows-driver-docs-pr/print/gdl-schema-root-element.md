---
title: GDL 架构根元素
description: GDL 架构根元素
keywords:
- GDL WDK，元素
- GDL WDK，架构
- SnapshotRoot 元素 WDK GDL
- 根元素 WDK GDL
- 快照 WDK GDL，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfc5b9f5f5a984150b53334b40fd5a833ba9dae4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835913"
---
# <a name="gdl-schema-root-element"></a>GDL 架构根元素


GDL 分析器生成的 XSD 架构定义 (SnapshotRoot) 的根元素 &lt; &gt; ，如下所示：

```cpp
    <element name="SnapshotRoot" type="gdl:GDL_RootType"/>

    <complexType name="GDL_RootType"  >
        <sequence>
            <any processContents="lax" minOccurs="0" maxOccurs="unbounded"/>
        </sequence>
    </complexType>
```

XSD 架构不允许 &lt; 任何 &gt; 元素与已定义的元素类型共存，因此分析器的架构使根元素的定义变得非常灵活。 尽管 XSD 架构是特意遗留的，但 &lt; SnapshotRoot &gt; 元素可以按任意顺序保留任意数量的 &lt; GDL \_ 属性 &gt; 或 &lt; 构造 &gt; 元素。 由于 GDL 语言注重最近定义的条目，因此 XML 快照中的元素外观通常与条目在 GDL 源文件中的外观相反。

&lt;SnapshotRoot &gt; 元素是快照文档中的最外面的元素，它包含快照中的所有其他元素。 &lt; &gt; 每个快照中只能有一个 SnapshotRoot 元素。

 

 




