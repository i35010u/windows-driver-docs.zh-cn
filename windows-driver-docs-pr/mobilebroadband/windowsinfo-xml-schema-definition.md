---
title: WindowsInfo XML 架构定义
description: WindowsInfo XML 架构定义
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 398cbf13054321557501260810366e2e49bee7c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832267"
---
# <a name="windowsinfo-xml-schema-definition"></a>WindowsInfo XML 架构定义

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

下面是 WindowsInfo XML 架构的命名空间：

``` syntax
http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/
http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2
```

下面是 WindowsInfo XML 架构的定义：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema targetNamespace="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/"
           xmlns:tns="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/"
           xmlns:v2="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2"
           xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

  <xs:element name="WindowsInfo" type="tns:WindowsInfoType" />

  <xs:complexType name="WindowsInfoType">
    <xs:sequence>
      <xs:element name="ShowDeviceInDisconnectedState" type="xs:boolean" default="false" />
      <xs:element name="LaunchDeviceStageOnDeviceConnect" type="xs:boolean" default="false" minOccurs="0" />
      <xs:element name="LaunchDeviceStageFromExplorer" type="xs:boolean" default="false" minOccurs="0" />
    </xs:sequence>
  </xs:complexType>

</xs:schema>
```

下面是 WindowsInfov2 XML 架构的定义：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema targetNamespace="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2"
           xmlns:tns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2"
           xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

  <xs:element name="LaunchApplicationOnDeviceConnect" type ="tns:LaunchApplicationOnDeviceConnectType" />
  <xs:element name="WindowsHardwareLogoCertified" type="tns:WindowsHardwareLogoCertifiedType" />
  <xs:element name="EnableAutoPlayForRegisteredApps" type="xs:boolean" default="false" />


  <!-- LaunchApplicationOnDeviceConnectType Definition-->
  <xs:complexType name="LaunchApplicationOnDeviceConnectType">
    <xs:choice>
      <xs:element name="AutoplayHandler" type="tns:AutoplayHandlerType" />
      <xs:element name="DesktopAutoplayHandler" type="xs:string" />
      <xs:any namespace="##other" processContents="lax" />
    </xs:choice>
  </xs:complexType>

  <!-- Autoplay Handler Type Definition-->
  <xs:complexType name="AutoplayHandlerType">
    <xs:sequence>
      <xs:element name="PackageIdentity" type="tns:PackageIdentityType" />
      <xs:element name="Application" type="tns:ApplicationType" />
      <xs:element name="Verb" type="tns:VerbType" />
      <xs:element name="AutoplayType" type="tns:AutoplayTypeType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>


<!-- Package Identity Type Definition -->
  <xs:complexType name="PackageIdentityType">
    <xs:attribute name="Name" type="tns:PackageNameType" use="required" />
    <xs:attribute name="Publisher" type="tns:PublisherType" use="required" />
  </xs:complexType>

  <xs:simpleType name="PackageNameType">
    <xs:restriction base="tns:AsciiIdentifierType">
      <xs:minLength value="3"/>
      <xs:maxLength value="50"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="AsciiIdentifierType">
    <xs:restriction base="tns:AllowedAsciiCharSetType">
      <xs:pattern value="[^_ ]+"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="PublisherType">
    <xs:restriction base="tns:DistinguishedNameType">
      <xs:maxLength value="8192"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="DistinguishedNameType">
    <xs:restriction base="tns:NonEmptyStringType">
      <xs:pattern value="(CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")(, ((CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")))*"/>
    </xs:restriction>
  </xs:simpleType>
  
  <xs:simpleType name="AutoplayTypeType">
    <xs:restriction base="xs:string">
       <xs:enumeration value="Device" />
       <xs:enumeration value="Content" />
    </xs:restriction>
  </xs:simpleType>

<!-- Applications Type Definition -->
  <xs:complexType name="ApplicationType">
    <xs:attribute name="Id" type="tns:ApplicationIdType" use="required"/>
  </xs:complexType>

  <xs:simpleType name="ApplicationIdType">
    <xs:restriction base="tns:AsciiWindowsIdType">
      <xs:maxLength value="64"/>
    </xs:restriction>
  </xs:simpleType>


  <!--AUTO-PLAY EXTENSION SCHEMA Types-->
  <xs:simpleType name="VerbType">
    <xs:restriction base="tns:AllowedAsciiCharSetType">
      <xs:pattern value="[^ ]+"/>
      <xs:maxLength value="64"/>
    </xs:restriction>
  </xs:simpleType>

  <!-- WindowsHardwareLogoCertifiedType Definition-->
  <xs:complexType name="WindowsHardwareLogoCertifiedType">
  </xs:complexType>
  
  <!-- String Restriction Types definition -->
  <xs:simpleType name="AllowedAsciiCharSetType">
    <xs:restriction base="tns:NonEmptyStringType">
      <xs:pattern value="[-_. A-Za-z0-9]+"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="AsciiWindowsIdType">
    <xs:restriction base="tns:NonEmptyStringType">
      <xs:pattern value="([A-Za-z][A-Za-z0-9]*)(\.[A-Za-z][A-Za-z0-9]*)*"/>
      <xs:maxLength value="255"/>
    </xs:restriction>
  </xs:simpleType>
  
  <xs:simpleType name="NonEmptyStringType">
    <xs:restriction base="xs:string">
      <xs:minLength value="1"/>
      <xs:maxLength value="32767"/>
      <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
    </xs:restriction>
  </xs:simpleType>
  
</xs:schema>
```
