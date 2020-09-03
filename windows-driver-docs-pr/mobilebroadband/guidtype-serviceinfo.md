---
title: 'GUIDType (ServiceInfo) '
description: 'GUIDType (ServiceInfo) '
ms.assetid: a08d4c7c-c282-4870-b836-6788ffa2d088
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50b6179569ef2616125bd1cdb1ff3e980a44a1f4
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402950"
---
# <a name="guidtype-serviceinfo"></a>GUIDType (ServiceInfo) 

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

GUIDType XML 简单类型指定一个 GUID。

``` syntax
<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idpatternsspanspan-idpatternsspanspan-idpatternsspanpatterns"></a><span id="Patterns"></span><span id="patterns"></span><span id="PATTERNS"></span>模式


GUIDType 简单类型为 **xs： string** ，受以下模式的限制：

-   \[0-9a-z-f-0-9a-z--9a-z--0-9a-z-- \] {8} \[ \] {4} \[ - \] {4} \[ \] {4} \[ -0--9a-z-f\]{12}

 

 





