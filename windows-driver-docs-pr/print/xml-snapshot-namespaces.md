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
ms.openlocfilehash: dcc840e67d0a1d348d9ab1fe64ad6364ee42e3c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355193"
---
# <a name="xml-snapshot-namespaces"></a>XML 快照命名空间


&lt;SnapshotRoot&gt; XML 快照中的元素定义快照命名空间，并将它们与 xsd、 xsi 和默认前缀关联。

```cpp
<SnapshotRoot xmlns="http://schemas.microsoft.com/2002/print/gdl/1.0"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
```

下面的代码示例演示&lt;架构&gt;由 GDL 分析器生成的 XSD 架构中的元素的开始标记。

```cpp
<schema
    xmlns="http://www.w3.org/2001/XMLSchema"
    xmlns:gdl="http://schemas.microsoft.com/2002/print/gdl/1.0"
    targetNamespace="http://schemas.microsoft.com/2002/print/gdl/1.0"
    elementFormDefault="qualified"
    attributeFormDefault="unqualified">
```

这些定义最小化使用的架构和快照中显式命名空间前缀的需求。 典型的用户不需要再也不用担心这些定义的含义。 您需要了解这些命名空间约定仅当你选择要使用\*数据类型：XSD\_定义。 有关模板作者的数据类型由使用提供的定义\*XSDTypeDefinition 指令应遵循的命名空间和中定义的默认值&lt;架构&gt;元素。 这些 XSD 的实例数据\_定义数据类型需要遵循的命名空间中定义的&lt;SnapshotRoot&gt;。

 

 




