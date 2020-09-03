---
title: 'GUIDType (PackageInfo) '
description: 'GUIDType (PackageInfo) '
ms.assetid: 3f88df5a-2a17-4006-ad3b-aab9a12cbcb9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d42545a4d2611e72b6b7960392ec88852b4460e3
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402884"
---
# <a name="guidtype-packageinfo"></a>GUIDType (PackageInfo) 

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

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


GUIDType XML 简单类型指定一个 GUID，用于唯一标识设备元数据包内的组件，例如设备的 [ExperienceID](experienceid.md)、 [LanguageNeutralIdentifier](languageneutralidentifier.md)和 [ModelID](modelid.md) 值。

 

 





