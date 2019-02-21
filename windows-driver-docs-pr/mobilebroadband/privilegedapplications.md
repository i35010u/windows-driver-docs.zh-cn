---
title: PrivilegedApplications
description: PrivilegedApplications
ms.assetid: fb0c4a7e-173e-4768-b1ba-a6c5149d61aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362f95feb82243a433469dafd86f5e0c9efd8460
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520664"
---
# <a name="privilegedapplications"></a>PrivilegedApplications

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PrivilegedApplications 元素指定的应用程序有权访问特权的移动宽带接口。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<PrivilegedApplications>
  Child elements
</PrivilegedApplications>
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
<td><p><a href="package-privapps.md" data-raw-source="[Package](package-privapps.md)">包</a></p></td>
<td><p>应该有权访问特权的移动宽带接口应用。</p></td>
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
<td><p><a href="softwareinfo.md" data-raw-source="[SoftwareInfo](softwareinfo.md)">SoftwareInfo</a></p></td>
<td><p>父元素<a href="softwareinfo-xml-schema.md" data-raw-source="[SoftwareInfo XML schema](softwareinfo-xml-schema.md)">SoftwareInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="PrivilegedApplications" type="tns:PrivilegedApplicationsType" minOccurs="0" />

<xs:complexType name="PrivilegedApplicationsType">
  <xs:choice>
    <xs:element name="AnyApplication" type="tns:AnyApplicationType" />
    <xs:element name="Package" type="tns:PackageForPrivilegedApplications" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:choice>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   PrivilegedApplications 元素允许指定的应用程序便可以使用特权访问的移动宽带和 SMS Api 访问权限。

-   包的结构[标识](identity-privapps.md)具有相同&lt;标识&gt;应用程序清单结构中的元素。 应将元素复制的应用程序清单。

-   若要指定多个包，请列出多个[包](package-privapps.md)PrivilegedApplications 元素中的元素。

-   包名称、 发布者和应用程序 ID 必须与匹配的 Microsoft Store 应用程序的 package.appxmanifest 中的信息。 发布服务器上也与 PC 安装的发布服务器证书必须匹配。

-   下面列出的 Microsoft Store 应用[DeviceCompanionApplications](devicecompanionapplications.md)元素具有访问特权移动宽带接口包括短信、 该应用还必须指定下 PrivilegedApplications元素。

-   当您要提交到 Windows 开发人员中心仪表板在服务元数据包时，您無法宣告 2 个以上的特权应用程序。 一个应用程序必须将自动下载的 Microsoft Store 设备应用的应用程序 ID。 第二个特权的应用不会自动下载，但如果安装了应用程序将访问特权的移动宽带 api。

PrivilegedApplications 元素是可选的。

 

 





