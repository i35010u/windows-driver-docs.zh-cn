---
title: GUIDType （ServiceInfo）
description: GUIDType （ServiceInfo）
ms.assetid: a08d4c7c-c282-4870-b836-6788ffa2d088
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b979649c213b7d7b515c34755477c041c2ae49bc
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323689"
---
# <a name="guidtype-serviceinfo"></a>GUIDType （ServiceInfo）

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

GUIDType XML 简单类型指定一个 GUID。

``` syntax
<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idpatternsspanspan-idpatternsspanspan-idpatternsspanpatterns"></a><span id="Patterns"></span><span id="patterns"></span><span id="PATTERNS"></span>模式


GUIDType 简单类型为**xs： string** ，受以下模式的限制：

-   \[0-9a-z-9a-z-F \] {8}-\[0--F \] {4} \[0 \]-9a-z--f {4} \[0 0-9a-z--f 1 20 3 4

 

 





