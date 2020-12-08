---
title: XML 快照命名空间
description: XML 快照命名空间
keywords:
- GDL WDK，命名空间
- SnapshotRoot 元素 WDK GDL
- 快照 WDK GDL，结构
- 快照 WDK GDL，命名空间
- 命名空间 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80c7a660f1a79e6211138776143b11b202928c2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785749"
---
# <a name="xml-snapshot-namespaces"></a>XML 快照命名空间


&lt; &gt; XML 快照中的 SnapshotRoot 元素定义快照命名空间，并将它们与 xsd、xsi 和 default 前缀关联。

```cpp
<SnapshotRoot xmlns="https://schemas.microsoft.com/2002/print/gdl/1.0"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">
```

下面的代码示例显示了 &lt; &gt; GDL 分析器生成的 XSD 架构中的架构元素开始标记。

```cpp
<schema
    xmlns="https://www.w3.org/2001/XMLSchema"
    xmlns:gdl="https://schemas.microsoft.com/2002/print/gdl/1.0"
    targetNamespace="https://schemas.microsoft.com/2002/print/gdl/1.0"
    elementFormDefault="qualified"
    attributeFormDefault="unqualified">
```

这些定义最大限度地减少了在架构和快照中使用显式命名空间前缀的需求。 典型用户无需担心这些定义的含意。 仅当你选择使用 \* DataType：已定义 XSD 时，才需要注意这些命名空间约定 \_ 。 对于模板作者，使用 XSDTypeDefinition 指令提供的数据类型定义 \* 应遵循在 schema 元素中定义的命名空间和默认值 &lt; &gt; 。 这些 XSD \_ 定义数据类型的实例数据需要遵循在 SnapshotRoot 中定义的命名空间 &lt; &gt; 。

 

 




