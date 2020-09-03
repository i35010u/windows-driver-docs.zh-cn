---
title: PrivilegedApplications
description: PrivilegedApplications
ms.assetid: fb0c4a7e-173e-4768-b1ba-a6c5149d61aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9caacb068bb226060a07e91725e84d65c941c67a
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403454"
---
# <a name="privilegedapplications"></a>PrivilegedApplications

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

PrivilegedApplications 元素指定将允许访问特权移动宽带接口的应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<PrivilegedApplications>
  Child elements
</PrivilegedApplications>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="package-privapps.md" data-raw-source="[Package](package-privapps.md)">包</a></p></td>
<td><p>应该有权访问特权移动宽带接口的应用。</p></td>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="softwareinfo.md" data-raw-source="[SoftwareInfo](softwareinfo.md)">SoftwareInfo</a></p></td>
<td><p><a href="softwareinfo-xml-schema.md" data-raw-source="[SoftwareInfo XML schema](softwareinfo-xml-schema.md)">SOFTWAREINFO XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


-   使用 PrivilegedApplications 元素，指定的应用可以使用特权访问权限访问移动宽带和 SMS Api。

-   包 [标识](identity-privapps.md) 的结构与 &lt; &gt; 应用程序清单结构中的标识元素相同。 你应从应用程序清单中复制元素。

-   若要指定多个包，请在 PrivilegedApplications 元素中列出多个 [包](package-privapps.md) 元素。

-   包名称、发布者和应用程序 ID 必须与 Microsoft Store 应用程序的 appxmanifest.xml 中的信息相匹配。 发布者还必须与电脑上安装的发布者证书匹配。

-   对于 [DeviceCompanionApplications](devicecompanionapplications.md) 元素下列出的 Microsoft Store 应用有权访问包括 SMS 的特权移动宽带接口，还必须在 PrivilegedApplications 元素下指定该应用。

-   将服务元数据包提交到 Windows 开发人员中心仪表板时，不能声明2个以上的特权应用。 应用中的一个应用必须是将自动下载 Microsoft Store 设备应用的应用 ID。 第二个特权应用程序不会自动下载，但是如果安装了应用程序，则将访问特权移动宽带 Api。

PrivilegedApplications 元素是可选的。

 

 





