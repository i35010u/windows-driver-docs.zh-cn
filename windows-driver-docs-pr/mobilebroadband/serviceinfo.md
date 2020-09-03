---
title: ServiceInfo
description: ServiceInfo
ms.assetid: 0dab9e5b-122c-4fe4-9314-97a0531af4aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a92cb4245f54fbfa51ea3522a44d76fbf95a431a
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403434"
---
# <a name="serviceinfo"></a>ServiceInfo

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

ServiceInfo 元素是 [SERVICEINFO XML 架构](serviceinfo-xml-schema.md)的父元素。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceInfo>
  child elements
</ServiceInfo>
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
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a></p></td>
<td><p>指定应用于服务的一个或多个功能类别。</p></td>
</tr>
<tr class="even">
<td><p><a href="servicename.md" data-raw-source="[ServiceName](servicename.md)">ServiceName</a></p></td>
<td><p>未使用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="servicedescription1.md" data-raw-source="[ServiceDescription1](servicedescription1.md)">ServiceDescription1</a></p></td>
<td><p>指定有关服务的描述性信息。 这适用于无线广域网 (WWAN) 连接配置文件的 "描述" 字段。 它不会在用户界面中显示给最终用户。</p></td>
</tr>
<tr class="even">
<td><p><a href="servicedescription2.md" data-raw-source="[ServiceDescription2](servicedescription2.md)">ServiceDescription2</a></p></td>
<td><p>未使用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="servicenumber.md" data-raw-source="[ServiceNumber](servicenumber.md)">ServiceNumber</a></p></td>
<td><p>这是一个自行生成的 GUID，用于标识正在提交此包的操作员。</p></td>
</tr>
<tr class="even">
<td><p><a href="serviceprovider.md" data-raw-source="[ServiceProvider](serviceprovider.md)">ServiceProvider</a></p></td>
<td><p>此名称在 Windows 连接管理器中显示为家庭网络显示名称。</p></td>
</tr>
<tr class="odd">
<td><p><a href="serviceiconfile.md" data-raw-source="[ServiceIconFile](serviceiconfile.md)">ServiceIconFile</a></p></td>
<td><p>指定服务的图标文件的名称。</p>
<div class="alert">
<strong>注意</strong><br/><p>在架构中，这会列为可选。 但是，在将包提交到 Windows 开发人员中心仪表板时，必须通过验证才能通过验证。</p>
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td><p><a href="servicespecificextension.md" data-raw-source="[ServiceSpecificExtension](servicespecificextension.md)">ServiceSpecificExtension</a></p></td>
<td><p>引用特定于此 ServiceCategory 的文件的位置。 对于 Windows 8、Windows 8.1 或适用于桌面版的 Windows 10 (Home、Pro、Enterprise 和教育) 服务元数据包，这是 MobileBroadbandInfo.xml 的位置。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


没有父元素。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


ServiceInfo 元素必须包含 [ServiceCategoryList](servicecategorylist.md)、 [ServiceNumber](servicenumber.md)、 [ServiceProvider](serviceprovider.md)和 [ServiceSpecificExtension](servicespecificextension.md) 元素的一个实例。

ServiceInfo 元素是必需的。









