---
title: 'GUIDType (ServiceInfo) '
description: 'GUIDType (ServiceInfo) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 607807d71edb6713dbb8165e6bac99da29b946e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782335"
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

 

 





