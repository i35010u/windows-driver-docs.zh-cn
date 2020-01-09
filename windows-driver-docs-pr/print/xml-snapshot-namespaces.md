---
title: XML 快照命名空间
description: XML 快照命名空间
ms.assetid: 723f1cfd-633c-4f87-b85f-5ccee45a8c4e
keywords:
- GDL WDK，命名空间
- SnapshotRoot 元素 WDK GDL
- 快照 WDK GDL，结构
- 快照 WDK GDL，命名空间
- 命名空间 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4c8c997a78288cad82da9d32179559ef71ee77b
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653015"
---
# <a name="xml-snapshot-namespaces"></a>XML 快照命名空间


XML 快照中的 &lt;SnapshotRoot&gt; 元素定义快照命名空间，并将它们与 xsd、xsi 和 default 前缀关联。

```cpp
<SnapshotRoot xmlns="https://schemas.microsoft.com/2002/print/gdl/1.0"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">
```

下面的代码示例演示了 GDL 分析器生成的 XSD 架构中的 &lt;架构&gt; 元素的开始标记。

```cpp
<schema
    xmlns="https://www.w3.org/2001/XMLSchema"
    xmlns:gdl="https://schemas.microsoft.com/2002/print/gdl/1.0"
    targetNamespace="https://schemas.microsoft.com/2002/print/gdl/1.0"
    elementFormDefault="qualified"
    attributeFormDefault="unqualified">
```

这些定义最大限度地减少了在架构和快照中使用显式命名空间前缀的需求。 典型用户无需担心这些定义的含意。 仅当选择使用 \*数据类型： XSD\_定义时，才需要注意这些命名空间约定。 对于模板作者，使用 \*XSDTypeDefinition 指令提供的数据类型定义应遵循 &lt;schema&gt; 元素中定义的命名空间和默认值。 这些 XSD\_定义数据类型的实例数据需要遵循 &lt;SnapshotRoot&gt;中定义的命名空间。

 

 




