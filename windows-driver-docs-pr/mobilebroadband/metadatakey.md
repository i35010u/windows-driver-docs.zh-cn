---
title: MetadataKey
description: MetadataKey
ms.assetid: 1915db47-98bb-40f5-be3b-75e9af80f506
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68b5b01565427bd1b8b0786f8f305c624a042a87
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902504"
---
# <a name="metadatakey"></a>MetadataKey

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MetadataKey 元素指定服务元数据包的属性。 其中包括：

- 设备支持的每个硬件功能的标识符。

- 包中的文本字符串的语言特定区域设置。

## <a name="usage"></a>使用情况

``` syntax
<MetadataKey>
  child elements
</MetadataKey>
```

## <a name="attributes"></a>属性

没有特性。

## <a name="child-elements"></a>子元素

|元素|说明|
|----|----|
|[HardwareIDList](hardwareidlist.md)|[HardwareIDList](hardwareidlist.md)元素指定设备的一个或多个硬件标识字符串。|
|[LastModifiedDate](lastmodifieddate.md)|[LastModifiedDate](lastmodifieddate.md)元素指定服务元数据包的上次更改时间戳。|[区域设置](locale.md)|[Locale](locale.md)元素指定服务元数据包的本地化版本。|
|[ModelIDList](modelidlist.md)|[ModelIDList](modelidlist.md)元素指定在服务元数据包中指定的每个设备类型或模型的 GUID。|
|[MultipleLocale](multiplelocale.md)|[MultipleLocale](multiplelocale.md)元素指定服务元数据包是否支持多个区域设置。|

## <a name="parent-elements"></a>父元素

|元素|说明|
|----|----|
|[PackageInfo](packageinfo.md)|[PackageInfo](packageinfo.md)元素是[PackageInfo XML 架构](packageinfo-xml-schema.md)的父元素。 PackageInfo 元素的子元素指定设备元数据包的属性。|

## <a name="xsd"></a>XSD

``` syntax
<xs:element name="MetadataKey" type="tns:MetadataKeyType" />

<xs:complexType name="MetadataKeyType">
  <xs:sequence>
    <xs:choice>
      <xs:sequence>
       <xs:element name="HardwareIDList" type="tns:HardwareIDListType" />
       <xs:element name="ModelIDList" type="tns:ModelIDListType" minOccurs="0" />
      </xs:sequence>
      <xs:element name="ModelIDList" type="tns:ModelIDListType" />
    </xs:choice>
    <xs:element name="Locale" type="tns:LocaleType" />
    <xs:element name="LastModifiedDate" type="xs:dateTime" />
    <xs:element ref="v2:MultipleLocale" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

下面是 PackageInfov2 XML 架构元数据：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema targetNamespace="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2"
           xmlns:tns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2"
           xmlns:xs="http://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified"
           blockDefault="#all">

<xs:element name="MultipleLocale" type ="xs:boolean" />

</xs:schema>
```

## <a name="remarks"></a>注解

MetadataKey 元素的子元素指定操作系统用于执行以下操作的元数据：

- 基于设备的 [ModelID](modelid.md) 或 [HardwareID](hardwareid.md) 值搜索服务元数据包的设备元数据存储。 如果有多个元数据包与设备的型号或硬件 ID 匹配，操作系统还会将元数据包内的 [区域设置](locale.md) 值与用户计算机上的当前语言设置进行比较。

- 如果包的 [LastModifiedDate](lastmodifieddate.md) 值比设备元数据存储中现有的包新，则使用服务元数据包更新设备元数据存储。

MetadataKey 元素必须包含：

- [Locale](locale.md)和[LastModifiedDate](lastmodifieddate.md)元素的一个实例。

- [HardwareIDList](hardwareidlist.md)或[ModelIDList](modelidlist.md)元素的一个实例。 MetadataKey 元素可以包含两个元素的一个实例。

MetadataKey 元素是必需的。
