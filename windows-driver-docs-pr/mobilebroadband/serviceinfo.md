---
title: ServiceInfo
description: ServiceInfo
ms.assetid: 0dab9e5b-122c-4fe4-9314-97a0531af4aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd4647a85856ed7d60cc5b6ae70348c9fe598cfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566086"
---
# <a name="serviceinfo"></a>ServiceInfo

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceInfo 元素是父元素[ServiceInfo XML 架构](serviceinfo-xml-schema.md)。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceInfo>
  child elements
</ServiceInfo>
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
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a></p></td>
<td><p>指定适用于服务的一个或多个功能类别。</p></td>
</tr>
<tr class="even">
<td><p><a href="servicename.md" data-raw-source="[ServiceName](servicename.md)">ServiceName</a></p></td>
<td><p>不使用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="servicedescription1.md" data-raw-source="[ServiceDescription1](servicedescription1.md)">ServiceDescription1</a></p></td>
<td><p>指定有关服务的描述性信息。 这被应用于无线广域网 (WWAN) 网络连接配置文件的说明字段。 它不显示给最终用户的用户界面。</p></td>
</tr>
<tr class="even">
<td><p><a href="servicedescription2.md" data-raw-source="[ServiceDescription2](servicedescription2.md)">ServiceDescription2</a></p></td>
<td><p>不使用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="servicenumber.md" data-raw-source="[ServiceNumber](servicenumber.md)">ServiceNumber</a></p></td>
<td><p>这是自生成的 GUID，用于标识正在提交此包的运算符。</p></td>
</tr>
<tr class="even">
<td><p><a href="serviceprovider.md" data-raw-source="[ServiceProvider](serviceprovider.md)">ServiceProvider</a></p></td>
<td><p>Windows 连接管理器中显示为家庭网络的显示名称。</p></td>
</tr>
<tr class="odd">
<td><p><a href="serviceiconfile.md" data-raw-source="[ServiceIconFile](serviceiconfile.md)">ServiceIconFile</a></p></td>
<td><p>在服务元数据包中指定服务图标文件的名称。</p>
<div class="alert">
<strong>注意</strong><br/><p>这是作为可选的架构中列出。 但是，它是为了通过验证包提交到 Windows 开发人员中心仪表板时所必需的。</p>
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td><p><a href="servicespecificextension.md" data-raw-source="[ServiceSpecificExtension](servicespecificextension.md)">ServiceSpecificExtension</a></p></td>
<td><p>引用特定于此 ServiceCategory 文件的位置。 对于 Windows 8、 Windows 8.1 或 Windows 10 桌面版 （主页、 专业版、 企业版和教育） 服务元数据包，这是 MobileBroadbandInfo.xml 的位置。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


没有父元素。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ServiceInfo" type="tns:ServiceInfoType" />

<xs:complexType name="ServiceInfoType">
  <xs:sequence>
    <xs:element name="ServiceCategoryList" type="tns:ServiceCategoryListType" />
    <xs:element name="ServiceName" type="tns:ServiceNameType" minOccurs="0" />
    <xs:element name="ServiceDescription1" type="tns:ServiceDescriptionType" minOccurs="0" />
    <xs:element name="ServiceDescription2" type="tns:ServiceDescriptionType" minOccurs="0" />
    <xs:element name="ServiceNumber" type ="tns:ServiceNumberType" />
    <xs:element name="ServiceProvider" type="tns:ProviderNameType" />
    <xs:element name="ServiceIconFile" type="tns:ServiceIconFileType" minOccurs="0" />
    <xs:element name="ServiceSpecificExtension" type="tns:ServiceSpecificExtensionType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ServiceInfo 元素必须包含的一个实例[ServiceCategoryList](servicecategorylist.md)， [ServiceNumber](servicenumber.md)， [ServiceProvider](serviceprovider.md)，和[ServiceSpecificExtension](servicespecificextension.md)元素。

ServiceInfo 元素是必需的。









