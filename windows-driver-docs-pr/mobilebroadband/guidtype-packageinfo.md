---
title: GUIDType (PackageInfo)
description: GUIDType (PackageInfo)
ms.assetid: 3f88df5a-2a17-4006-ad3b-aab9a12cbcb9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56c027f7cbf898c7ff6035974eba89d08d0a0ea0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520869"
---
# <a name="guidtype-packageinfo"></a>GUIDType (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

GUIDType XML 简单类型指定的 GUID。

``` syntax
<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idpatternsspanspan-idpatternsspanspan-idpatternsspanpatterns"></a><span id="Patterns"></span><span id="patterns"></span><span id="PATTERNS"></span>模式


GUIDType 简单类型是**xs: string**受以下模式：

-   \[0-9a-fA-F\]{8}-\[0-9a-fA-F\]{4}-\[0-9a-fA-F\]{4}-\[0-9a-fA-F\]{4}-\[0-9a-fA-F\]{12}

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


GUIDType XML 简单类型指定唯一标识设备元数据包，如设备中的组件的 GUID [ExperienceID](experienceid.md)， [LanguageNeutralIdentifier](languageneutralidentifier.md)，并且[ModelID](modelid.md)值。

 

 





