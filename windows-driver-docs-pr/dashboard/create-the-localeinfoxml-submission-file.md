---
title: 创建 LocaleInfo.xml 提交文件
description: 创建 LocaleInfo.xml 提交文件
ms.assetid: 2b16b045-4d34-418c-8f68-7f688adf8e7e
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5115e3116dac7a99de071fa37cfdc886cbdeb57d
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802805"
---
# <a name="create-the-localeinfoxml-submission-file"></a>创建 LocaleInfo.xml 提交文件

## <a name="localeinfo-xml-schema"></a>LocaleInfo XML 架构

设备清单提交包必须包含一个 LocaleInfo.xml 文档，合作伙伴中心使用其中包含的信息来验证设备元数据包中的区域设置信息。

LocaleInfo.xml 文档中的数据基于 LocaleInfo XML 架构（将在下面进行介绍）设置格式。

> [!NOTE]
> 该 XML 文档必须使用 UTF-8 编码进行保存。

有关地址范围的详细信息，请参阅[如何为设备和打印机创建设备元数据包](https://go.microsoft.com/fwlink/?LinkId=253559)。

### <a name="localeinfo-xml-schema-namespace"></a>LocaleInfo XML 架构命名空间

以下是 LocaleInfo XML 架构的命名空间：`http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo`

### <a name="overview-of-localeinfo-xml-elementsattributes"></a>LocaleInfo XML 元素/属性概述

下表描述 LocaleInfo XML 架构的元数据元素和属性。

|元素/属性|元素/属性类型|必需/可选|
|----|----|----|
|MultipleLocale|xs:boolean|可选|
|LocaleDeclaredInPackageInfo|tns:LocaleDeclaredInPackageInfoType|可选|
|默认|xs:boolean|必需|
|SupportedLocaleList|tns:SupportedLocaleListType|可选|
|Locale|xs:string|可选|

### <a name="localeinfo-xml-schema-definition"></a>LocaleInfo XML 架构定义

以下是 LocaleInfo XML 架构定义：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo" xmlns:tns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

 <xs:element name="LocaleInfo" type="tns:LocaleInfoType" />

 <xs:complexType name="LocaleInfoType">
  <xs:sequence>
   <xs:element name="MultipleLocale" type="xs:boolean" />
   <xs:element name="LocaleDeclaredInPackageInfo" type="tns:LocaleDeclaredInPackageInfoType" />
   <xs:element name="SupportedLocaleList" type="tns:SupportedLocaleListType" minOccurs="0" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

  <xs:complexType name="LocaleDeclaredInPackageInfoType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="default" type="xs:boolean" use="required" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>

  <xs:complexType name="SupportedLocaleListType">
    <xs:sequence>
      <xs:element name="Locale" type="xs:string" maxOccurs="unbounded" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

</xs:schema>
```

## <a name="localeinfo-xml-schema-reference"></a>LocaleInfo XML 架构参考

LocaleInfo XML 架构定义以下元素和属性：

- LocaleInfo
  - MultipleLocale
  - LocaleDeclaredInPackageInfo
    - 默认
  - SupportedLocaleList
    - Locale

### <a name="multiplelocale-element"></a>MultipleLocale 元素

MultipleLocale 元素指定设备元数据包是否支持多个区域设置。 合作伙伴中心使用此值可正确验证包。

``` syntax
<xs:element name="MultipleLocale" type="xs:boolean" />
```

#### <a name="remarks-multiplelocale-element"></a>备注（MultipleLocale 元素）

如果在设备元数据包中支持多个区域设置，则 MultipleLocale 元素必须为“true”。 如果设备元数据包仅支持一个区域设置，则该元素可以为“true”或“false”。 MultipleLocale 的值必须匹配在 PackageInfo.xml 中指定的值。

### <a name="localedeclaredinpackageinfo-element"></a>LocaleDeclaredInPackageInfo 元素

LocaleDeclaredInPackageInfo 元素指定有关在设备元数据包中声明的区域设置和程序包属性的信息。 合作伙伴中心使用此信息可正确验证设备元数据包中的已声明区域设置元数据。

``` syntax
<xs:element name="LocaleDeclaredInPackageInfo" type="tns:LocaleDeclaredInPackageInfoType" />

<xs:complexType name="LocaleDeclaredInPackageInfoType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="default" type="xs:boolean" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

#### <a name="remarks-localedeclaredinpackageinfo-element"></a>备注（LocaleDeclaredInPackageInfo 元素）

LocaleDeclaredInPackageInfo 元素必须匹配在 PackageInfo.xml 中指定的区域设置值。

### <a name="default-attribute"></a>default 属性

default 属性指定设备元数据包是否为默认包，如 PackageInfo.xml 中所示。

``` syntax
<xs:attribute name="default" type="xs:boolean" use="required" />
```

#### <a name="remarks-default-element"></a>备注（默认元素）

default 元素必须匹配在 PackageInfo.xml 中指定的默认值。

### <a name="supportedlocalelist-element"></a>SupportedLocaleList 元素

SupportedLocaleList 元素指定在设备元数据包中支持哪些其他区域设置。 合作伙伴中心使用此信息可正确验证设备元数据包中的其他区域设置元数据。

``` syntax
<xs:element name="SupportedLocaleList" type="tns:SupportedLocaleListType" minOccurs="0" />

<xs:complexType name="SupportedLocaleListType">
  <xs:sequence>
    <xs:element name="Locale" type="xs:string" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

### <a name="locale-element"></a>Locale 元素

Locale 元素指定在设备元数据包中支持的额外区域设置。 有关合作伙伴中心如何使用此值的详细信息，请参阅“SupportedLocaleList 元素”。

## <a name="localeinfo-xml-example"></a>LocaleInfo XML 示例

以下 XML 文档使用 LocaleInfo XML 架构来指定 LocaleInfo 信息的组成部分。

此示例适用于支持 en-US、ja-JP 和 fr-FR 区域设置的设备元数据包。 它列出了 PackageInfo.xml 中的 en-US 区域设置，并且是默认区域设置包，如 PackageInfo.xml 中所示。

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<LocaleInfo xmlns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo">
  
  <MultipleLocale>
    true
  </MultipleLocale>
  
  <LocaleDeclaredInPackageInfo default="true">
    en-US
  </LocaleDeclaredInPackageInfo>
  
  <SupportedLocaleList>
    <Locale>en-US</Locale>
    <Locale>ja-JP</Locale>
    <Locale>fr-FR</Locale>
  </SupportedLocaleList>
  
</LocaleInfo>
```
