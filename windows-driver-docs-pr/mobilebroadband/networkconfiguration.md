---
title: NetworkConfiguration
description: NetworkConfiguration
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f70ab6f24e03b210d4b84e9145964fcd0e4de76
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805275"
---
# <a name="networkconfiguration"></a>NetworkConfiguration

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

NetworkConfiguration 元素指定要使用的购买和 Internet 移动宽带配置文件。 此元素中引用的文件应包含在 **ServiceInformation** 目录中。 这些文件有助于获取连接到操作员网络的用户。 它还指定是否应允许标准用户对其移动宽带 Sim 执行 PIN 解锁操作。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<NetworkConfiguration>
  child elements
</NetworkConfiguration>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p>指定要使用的购买和 Internet 移动宽带配置文件。</p></td>
</tr>
<tr class="even">
<td><p><a href="allowstandarduserpinunlock.md" data-raw-source="[AllowStandardUserPinUnlock](allowstandarduserpinunlock.md)">AllowStandardUserPinUnlock</a></p></td>
<td><p>指定是否允许标准用户对其移动宽带 Sim 执行 PIN 解锁操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


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
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a>元素是<a href="mobilebroadbandinfo-xml-schema.md" data-raw-source="[MobileBroadbandInfo XML schema](mobilebroadbandinfo-xml-schema.md)">MobileBroadbandInfo XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


-   为了设置计划购买 APN 或 Internet 连接 APN，移动网络操作员 (o) 应将与这些状态相对应的 XML 配置文件指定为此元素的一部分。

-   此元素中的子元素是可选的。 如果未指定这些值，则将使用 Windows 附带的 APN 数据库中的 APN 值来帮助用户进行连接。

-   通常，只有 Administrators 安全组中的用户可以对其移动宽带 Sim 执行 PIN 解锁操作。 但是，如果将 [AllowStandardUserPinUnlock](allowstandarduserpinunlock.md) 元素设置为 true，则允许移动运营商指定是否允许标准用户执行此功能。

 

 





