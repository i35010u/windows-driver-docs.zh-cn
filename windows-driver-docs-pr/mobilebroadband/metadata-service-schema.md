---
title: 元数据
description: 元数据
ms.assetid: bab7803c-df1f-4282-a9d7-5536d30d00dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fdd31bab9ea198ec707da98bcc99868f7646e66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576352"
---
# <a name="metadata"></a>元数据

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

元数据元素在服务元数据包中指定所引用的 XML 架构的命名空间。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Metadata
  MetadataID = "xs:anyURI">
  text
</Metadata>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MetadataID</p></td>
<td><p>xs: anyuri</p></td>
<td><p>是</p></td>
<td><p>指定服务元数据包中引用的 XML 架构的命名空间。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


服务元数据 XML 架构的命名空间的统一资源标识符 (URI)。 XML 架构必须是一个服务元数据包中引用的架构。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

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
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a></p></td>
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a>元素指定的 XML 架构的引用的服务元数据包。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="PackageStructure" type="tns:PackageStructureType" />

<xs:complexType name="PackageStructureType">
   <xs:sequence>
     <xs:element name="Metadata" type="tns:MetadataType" minOccurs="3" maxOccurs="unbounded" />
   </xs:sequence>
</xs:complexType>

<xs:complexType name="MetadataType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="MetadataID" type="xs:anyURI" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


在中[PackageInfo](packageinfo.md)元素中，必须指定元素的元数据的两个实例的最小值。 每个实例必须指定一个用于创建服务元数据包的以下所需 XML 架构的命名空间：

-   [PackageInfo XML 架构](packageinfo-xml-schema.md)

-   [ServiceInfo XML 架构](serviceinfo-xml-schema.md)

-   [WindowsInfo XML 架构](windowsinfo-xml-schema.md)

-   [SoftwareInfo XML 架构](softwareinfo-xml-schema.md)

最简单方法是将上面的以下示例复制到 Packageinfo.xml 文件。 如果任何上面指定的文件夹不包含在服务元数据包，请务必删除中的元数据元素[PackageStructure](packagestructure.md)元素。

``` syntax
<PackageStructure>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11">PackageInfo.xml</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/05/DeviceMetadata/ServiceInfo">ServiceInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">SoftwareInformation</Metadata>
</PackageStructure>
```

在运行 Windows 7 设备上不支持 SoftwareInformation 文件夹和服务元数据包。

每个文件夹名称可以更改为任意名称，只要此元数据元素中设置的名称。 下面的示例演示如何使用"WindowsInfo"作为文件夹名称：

``` syntax
<Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInfo</Metadata>
```

 

 





