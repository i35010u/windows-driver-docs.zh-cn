---
title: 元数据
description: 元数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f680c73046cd4545a56aa2a38e42afb747bb0032
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818421"
---
# <a name="metadata"></a>元数据

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

Metadata 元素指定服务元数据包中所引用的 XML 架构的命名空间。

## <a name="usage"></a>使用情况

``` syntax
<Metadata
  MetadataID = "xs:anyURI">
  text
</Metadata>
```

## <a name="attributes"></a>特性

|属性|类型|必须|描述|
|----|----|----|----|
|MetadataID|xs:anyURI|是|指定在服务元数据包内引用的 XML 架构的命名空间。|

## <a name="text-value"></a>文本值

服务元数据 XML 架构的命名空间 (URI) 的统一资源标识符。 XML 架构必须是服务元数据包内引用的架构之一。

## <a name="child-elements"></a>子元素

没有任何子元素。

## <a name="parent-elements"></a>父元素

|元素|描述|
|----|----|
|[PackageStructure](packagestructure.md)|[PackageStructure](packagestructure.md)元素指定服务元数据包引用的 XML 架构。|

## <a name="xsd"></a>XSD

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

## <a name="remarks"></a>备注

在 [PackageInfo](packageinfo.md) 元素中，必须至少指定 Metadata 元素的两个实例。 每个实例都必须指定以下一个用于创建服务元数据包的必需 XML 架构的命名空间：

- [PackageInfo XML 架构](packageinfo-xml-schema.md)

- [ServiceInfo XML 架构](serviceinfo-xml-schema.md)

- [WindowsInfo XML 架构](windowsinfo-xml-schema.md)

- [SoftwareInfo XML 架构](softwareinfo-xml-schema.md)

最简单的方法是将下面的示例复制到 Packageinfo.xml 文件中。 如果在服务元数据包中未包含以上指定的任何文件夹，请确保从 [PackageStructure](packagestructure.md) 元素中删除 metadata 元素。

``` syntax
<PackageStructure>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11">PackageInfo.xml</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/05/DeviceMetadata/ServiceInfo">ServiceInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">SoftwareInformation</Metadata>
</PackageStructure>
```

在运行 Windows 7 的设备上不支持 SoftwareInformation 文件夹和服务元数据包。

只要在此元数据元素中设置了名称，就可以将每个文件夹名称更改为任意名称。 下面的示例演示如何使用 "WindowsInfo" 作为文件夹名称：

``` syntax
<Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInfo</Metadata>
```
