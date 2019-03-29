---
title: NetworkConfiguration
description: NetworkConfiguration
ms.assetid: 4a52b185-1bfb-4626-99fb-6be364e88e85
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb69630c124c238fa920e45d1d87f1e4fc2cd687
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575505"
---
# <a name="networkconfiguration"></a>NetworkConfiguration

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

NetworkConfiguration 元素指定的采购和 Internet 移动宽带配置文件使用。 在此元素中引用的文件应包含在**ServiceInformation**目录。 这些文件可帮助在获取连接到运营商网络的用户。 它还指定是否应允许标准用户执行 PIN 解锁其移动宽带 SIMs 上的操作。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<NetworkConfiguration>
  child elements
</NetworkConfiguration>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mobilebroadbandprofiles.md" data-raw-source="[MobileBroadbandProfiles](mobilebroadbandprofiles.md)">MobileBroadbandProfiles</a></p></td>
<td><p>指定的采购和 Internet 移动宽带配置文件使用。</p></td>
</tr>
<tr class="even">
<td><p><a href="allowstandarduserpinunlock.md" data-raw-source="[AllowStandardUserPinUnlock](allowstandarduserpinunlock.md)">AllowStandardUserPinUnlock</a></p></td>
<td><p>指定是否应允许标准用户执行 PIN 解锁其移动宽带 SIMs 上的操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a></p></td>
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a>元素是父元素<a href="mobilebroadbandinfo-xml-schema.md" data-raw-source="[MobileBroadbandInfo XML schema](mobilebroadbandinfo-xml-schema.md)">MobileBroadbandInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="NetworkConfiguration" type="tns:NetworkConfigType" minOccurs="0" />

<xs:complexType name="NetworkConfigType">
  <xs:sequence>
    <xs:element name="MobileBroadbandProfiles" type="tns:MobileBroadbandProfilesType" minOccurs="0" />
    <xs:element name="AllowStandardUserPinUnlock" type="xs:boolean" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   若要设置计划购买 APN 或 Internet 连接 APN，移动网络运营商 (MNO) 应指定为此元素的一部分对应于为这些状态的 XML 配置文件。

-   在此元素中的子元素是可选的。 如果未指定这些，从包含 Windows APN 数据库 APN 值用于帮助用户进行连接。

-   通常情况下，只有用户在管理员安全组允许执行 PIN 解锁其移动宽带 SIMs 上的操作。 但是，将设置[AllowStandardUserPinUnlock](allowstandarduserpinunlock.md)为 true 的元素允许移动运营商来指定是否允许标准用户来执行此功能。

 

 





