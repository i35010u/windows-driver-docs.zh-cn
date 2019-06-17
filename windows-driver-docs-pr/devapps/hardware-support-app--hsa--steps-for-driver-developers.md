---
title: 硬件驱动程序开发人员支持应用程序 (HSA) 的步骤
description: 创建自定义能力对驱动程序与硬件支持应用程序 (HSA)
keywords:
- 自定义功能
- UWP 应用
- 自定义功能
- UWP
- 硬件
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fddb468087e7068dace633c9f3d7a5df5a84b861
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67047043"
---
# <a name="hardware-support-app-hsa-steps-for-driver-developers"></a>硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤

硬件支持应用程序 (HSA) 是一种特定于设备的应用，与特定的驱动程序配对或[RPC （远程过程调用）](https://msdn.microsoft.com/library/windows/desktop/aa378651)终结点。

若要将驱动程序与关联的应用商店应用，首先保留名为自定义功能的特殊值。 然后允许访问的播发功能和应用开发人员提供的功能的应用。  此页为驱动程序开发人员介绍这些步骤。

应用程序开发人员的步骤所述[硬件支持应用程序 (HSA):适用于应用开发人员的步骤](hardware-support-app--hsa--steps-for-app-developers.md)。

HSA 是四个 ("DCHU") 设计原则之一[通用 Windows 驱动程序](../develop/getting-started-with-universal-drivers.md)。

## <a name="reserving-a-custom-capability"></a>保留自定义功能

首先，保留自定义功能：

1.  Microsoft 硬件支持应用评审的电子邮件 (<HSAReview@microsoft.com>) 包含以下信息：

    * 联系信息
    * 公司名称
    * 功能名称 （必须是唯一的并且引用所有者）
    * 功能需要访问哪些资源？
    * 任何安全或隐私问题
    * 将到合作伙伴处理数据的哪些事件？
      * 将这些事件包括个人标识符，例如精确的用户的位置，密码，IP 地址，PUID、 设备 ID、 CID、 用户名和联系人数据）？
      * 数据事件持续用户在设备上，或它发送到合作伙伴？
    * 哪些数据容量，即提供对访问权限？
    * 为此功能的最终用户带来的好处是什么？
    * 包括 Microsoft Store 应用发布者 id。  若要获取该帐户，请 Microsoft Store 页上创建主干应用程序条目。 保留应用 PFN 的详细信息，请参阅[创建你的应用保留名称](https://msdn.microsoft.com/windows/uwp/publish/create-your-app-by-reserving-a-name)。

2.  如果请求得到批准，Microsoft 的电子邮件返回唯一的自定义功能字符串名称，格式**CompanyName.capabilityName\_PublisherID**。

现在可以使用自定义功能以允许访问的 RPC 终结点或驱动程序。

## <a name="allowing-access-to-an-rpc-endpoint-to-a-uwp-app-using-the-custom-capability"></a>允许访问到 UWP 应用使用自定义功能的 RPC 终结点

若要允许访问具有自定义功能的 UWP 应用的 RPC 终结点，请执行以下步骤：

1.  调用[ **DeriveCapabilitySidsFromName** ](https://msdn.microsoft.com/library/windows/desktop/mt803273)将自定义功能名称转换为安全 ID (SID)。
2.  将 SID 添加到您允许以及任何其他所需的 RPC 终结点的安全描述符的 Sid 的 ACE 的访问权限。
3.  创建使用安全描述符中的信息的 RPC 终结点。

您可以看到的更高版本中实现[RPC 服务器代码](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/CustomCapability/Service/Server/RpcServer.cpp)中[自定义功能示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)。

## <a name="allowing-access-to-a-driver-to-a-uwp-app-using-the-custom-capability"></a>允许访问到 UWP 应用使用自定义功能的驱动程序

若要允许访问驱动程序添加到 UWP 应用，而自定义功能，到 INF 文件或驱动程序源添加几行。

在 INF 文件中，指定自定义功能，如下所示：

```cpp
[WDMPNPB003_Device.NT.Interfaces] 
AddInterface= {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz},,AddInterfaceSection 
 
[AddInterfaceSection] 
AddProperty= AddInterfaceSection.AddProps 
 
[AddInterfaceSection.AddProps] 
; DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities 
{026e516e-b814-414b-83cd-856d6fef4822}, 8, 0x2012,, "CompanyName.myCustomCapabilityNameTBD_MyStorePubId"
```

或者，执行以下操作在驱动程序中：

```c++
WDF_DEVICE_INTERFACE_PROPERTY_DATA PropertyData = {}; 
WCHAR customCapabilities[] = L”CompanyName.myCustomCapabilityNameTBD_MyStorePubId\0”; 
 
WDF_DEVICE_INTERFACE_PROPERTY_DATA_INIT( 
   &PropertyData, 
   &m_VendorDefinedSubType, 
   &DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities); 
 
Status = WdfDeviceAssignInterfaceProperty( 
    m_FxDevice, 
    &PropertyData, 
    DEVPROP_TYPE_STRING_LIST, 
    ARRAYSIZE(customCapabilities), 
    reinterpret_cast<PVOID>(customCapabilities)); 

```

替换为`zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz`与要公开的接口的 GUID。  替换*CompanyName*公司名称， *myCustomCapabilityNameTBD*在你的公司中是唯一的名称和*MyStorePubId*与发布服务器存储 id。 

上面显示的驱动程序代码的示例，请参阅[驱动程序的通用驱动程序的包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)。

## <a name="preparing-the-signed-custom-capability-descriptor-sccd-file"></a>准备已签名自定义功能描述符 (SCCD) 文件

签名的自定义功能描述符 (SCCD) 文件是授权的一个或多个自定义功能使用已签名的 XML 文件。  驱动程序或 RPC 终结点的所有者授予应用程序开发人员，自定义功能允许通过提供此文件。

若要准备 SCCD 文件，首先更新自定义功能字符串。  使用下面的示例作为起点：

```xml
<?xml version="1.0" encoding="utf-8"?>
<CustomCapabilityDescriptor xmlns="http://schemas.microsoft.com/appx/2016/sccd" xmlns:s="http://schemas.microsoft.com/appx/2016/sccd">
<CustomCapabilities>
    <CustomCapability Name="microsoft.hsaTestCustomCapability_q536wpkpf5cy2"></CustomCapability>
</CustomCapabilities>
<AuthorizedEntities>
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
</AuthorizedEntities>
<Catalog>0000</Catalog>
</CustomCapabilityDescriptor>
```

接下来，自定义功能所有者获取包系列名称 (PFN) 和签名哈希从应用程序开发人员，并更新 SCCD 文件中的这些字符串。

**注意：** 应用程序无需直接使用该证书进行签名，但指定的证书必须是对应用进行签名的证书链的一部分。

完成后 SCCD，功能所有者电子邮件发送给 Microsoft 进行签名。  Microsoft 返回签名的 SCCD 功能所有者。

然后，功能所有者将 SCCD 发送到应用程序开发人员。  应用程序开发人员在应用程序清单中包含签名的 SCCD。  若要了解应用程序开发人员需要执行操作，请参阅[硬件支持应用程序 (HSA):适用于应用开发人员的步骤](hardware-support-app--hsa--steps-for-app-developers.md)。

## <a name="limiting-the-scope-of-an-sccd"></a>SCCD 作用域限制

出于测试目的，自定义功能所有者可以限制对开发人员模式中的计算机的硬件支持应用程序的安装。

若要执行此操作，获取由 Microsoft 签名 SCCD 之前，添加**DeveloperModeOnly**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<CustomCapabilityDescriptor xmlns="http://schemas.microsoft.com/appx/2016/sccd" xmlns:s="http://schemas.microsoft.com/appx/2016/sccd">
<CustomCapabilities>
    <CustomCapability Name="microsoft.hsaTestCustomCapability_q536wpkpf5cy2"></CustomCapability>
</CustomCapabilities>
<AuthorizedEntities>
    <AuthorizedEntity AppPackageFamilyName="MicrosoftHSATest.Microsoft.SDKSamples.Hsa.CPP_q536wpkpf5cy2" CertificateSignatureHash="ca9fc964db7e0c2938778f4559946833e7a8cfde0f3eaa07650766d4764e86c4"></AuthorizedEntity>
</AuthorizedEntities>
<Catalog>0000</Catalog>
<DeveloperModeOnly Value="true" />
</CustomCapabilityDescriptor>
```

生成签名中的设备上仅 SCCD works[开发人员模式](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)。 

## <a name="allowing-any-app-to-use-a-custom-capability"></a>允许任何应用程序以使用自定义功能

我们建议指定经过授权的实体 （应用），可以使用自定义功能。 在某些情况下，但是，你可能想要允许任何应用以包含 SCCD。  从 Windows 10 版本 1809年开始，你可以执行此操作通过添加**AllowAny** AuthorizedEntities 元素。 由于最佳做法是声明 SCCD 文件中经过授权的实体，请提供使用的理由**AllowAny**时提交你 SCCD 由 Microsoft 进行签名。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CustomCapabilityDescriptor xmlns="http://schemas.microsoft.com/appx/2018/sccd" xmlns:s="http://schemas.microsoft.com/appx/2018/sccd">
<CustomCapabilities>
    <CustomCapability Name="microsoft.hsaTestCustomCapability_q536wpkpf5cy2"></CustomCapability>
</CustomCapabilities>
<AuthorizedEntities AllowAny="true"/>
<Catalog>0000</Catalog>
</CustomCapabilityDescriptor>
```

生成签名的 SCCD 将验证在任何应用程序包中。 

## <a name="multiple-sccds"></a>多个 SCCDs

从 Windows 10 1803年版开始，应用程序可以声明一个或多个 SCCD 文件中的自定义功能。 将 SCCD 文件放在应用程序包的根目录中。

## <a name="summary"></a>总结

下图总结了前面所述的序列：

![获取签名 SCCD](images/signsccd.png)

## <a name="see-also"></a>请参阅

* [通用 Windows 驱动程序入门](../develop/getting-started-with-universal-drivers.md)
* [通用 Windows 平台简介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)
* [通用 Windows 平台 (UWP)](https://docs.microsoft.com/windows/uwp/design/basics/design-and-ui-intro)
* [应用程序功能](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)
* [开发使用 Visual Studio 的 UWP 应用](https://developer.microsoft.com/windows/apps/develop)
* [配对的驱动程序有一个通用 Windows 平台 (UWP) 应用程序](../install/pairing-app-and-driver-versions.md)
* [开发 UWP 应用](https://developer.microsoft.com/windows/apps/develop)
* [打包应用程序使用 Desktop App Converter （桌面桥）](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-run-desktop-app-converter)
* [自定义功能的示例应用](https://go.microsoft.com/fwlink/p/?LinkId=846904)
* [自定义功能驱动程序示例](https://aka.ms/customcapabilitydriversample )
* [旁加载 Windows 10 中的应用程序](https://technet.microsoft.com/library/mt269549.aspx)
* [有关自定义功能的常见问题解答](FAQ-on-custom-capabilities.md)

## <a name="sccd-xml-schema"></a>SCCD XML 架构

下面是 SCCD 文件的正式 XML XSD 架构。  使用此架构验证您 SCCD 再将其提交进行审阅。  请参阅[架构缓存](https://docs.microsoft.com/visualstudio/xml-tools/schema-cache)并[XML 文档验证](https://docs.microsoft.com/visualstudio/xml-tools/xml-document-validation)有关导入的架构和验证 IntelliSense 信息。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
  xmlns:xs="http://www.w3.org/2001/XMLSchema"
  targetNamespace="http://schemas.microsoft.com/appx/2016/sccd"
  xmlns:s="http://schemas.microsoft.com/appx/2016/sccd"
  xmlns="http://schemas.microsoft.com/appx/2016/sccd">

  <xs:element name="CustomCapabilityDescriptor" type="CT_CustomCapabilityDescriptor">
    <xs:unique name="Unique_CustomCapability_Name">
      <xs:selector xpath="s:CustomCapabilities/s:CustomCapability"/>
      <xs:field xpath="@Name"/>
    </xs:unique>
  </xs:element>

  <xs:complexType name="CT_CustomCapabilityDescriptor">
    <xs:sequence>
      <xs:element ref="CustomCapabilities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="AuthorizedEntities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="DeveloperModeOnly" minOccurs="0" maxOccurs="1"/>
      <xs:element ref="Catalog" minOccurs="1" maxOccurs="1"/>
      <xs:any minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="CustomCapabilities" type="CT_CustomCapabilities" />

  <xs:complexType name="CT_CustomCapabilities">
    <xs:sequence>
      <xs:element ref="CustomCapability" minOccurs="1" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="CustomCapability">
    <xs:complexType>
      <xs:attribute name="Name" type="ST_CustomCapability" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:simpleType name="ST_NonEmptyString">
    <xs:restriction base="xs:string">
      <xs:minLength value="1"/>
      <xs:maxLength value="32767"/>
      <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="ST_CustomCapability">
    <xs:annotation>
      <xs:documentation>Custom capabilities should be a string in the form of Company.capabilityName_PublisherId</xs:documentation>
    </xs:annotation>
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Za-z0-9][-_.A-Za-z0-9]*_[a-hjkmnp-z0-9]{13}"/>
      <xs:minLength value="15"/>
      <xs:maxLength value="255"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="AuthorizedEntities" type="CT_AuthorizedEntities" />

  <xs:complexType name="CT_AuthorizedEntities">
    <xs:sequence>
      <xs:element ref="AuthorizedEntity" minOccurs="1" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="AuthorizedEntity" type="CT_AuthorizedEntity" />

  <xs:complexType name="CT_AuthorizedEntity">
    <xs:attribute name="CertificateSignatureHash" type="ST_CertificateSignatureHash" use="required"/>
    <xs:attribute name="AppPackageFamilyName" type="ST_NonEmptyString" use="required"/>
  </xs:complexType>

  <xs:simpleType name="ST_CertificateSignatureHash">
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Fa-f0-9]+"/>
      <xs:minLength value="64"/>
      <xs:maxLength value="64"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="DeveloperModeOnly">
    <xs:complexType>
      <xs:attribute name="Value" type="xs:boolean" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:element name="Catalog" type="ST_Catalog" />

  <xs:simpleType name="ST_Catalog">
    <xs:restriction base="xs:string">
      <xs:pattern value="[A-Za-z0-9\+\/\=]+"/>
      <xs:minLength value="4"/>
    </xs:restriction>
  </xs:simpleType>

</xs:schema>
```

以下架构也是有效截止期为 Windows 10，版本 1809年的。  这样，SCCD 声明任何应用程序包，以便进行授权的实体。 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
  xmlns:xs="http://www.w3.org/2001/XMLSchema"
  targetNamespace="http://schemas.microsoft.com/appx/2018/sccd"
  xmlns:s="http://schemas.microsoft.com/appx/2018/sccd"
  xmlns="http://schemas.microsoft.com/appx/2018/sccd">

  <xs:element name="CustomCapabilityDescriptor" type="CT_CustomCapabilityDescriptor">
    <xs:unique name="Unique_CustomCapability_Name">
      <xs:selector xpath="s:CustomCapabilities/s:CustomCapability"/>
      <xs:field xpath="@Name"/>
    </xs:unique>
  </xs:element>

  <xs:complexType name="CT_CustomCapabilityDescriptor">
    <xs:sequence>
      <xs:element ref="CustomCapabilities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="AuthorizedEntities" minOccurs="1" maxOccurs="1"/>
      <xs:element ref="DeveloperModeOnly" minOccurs="0" maxOccurs="1"/>
      <xs:element ref="Catalog" minOccurs="1" maxOccurs="1"/>
      <xs:any minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
  
  <xs:element name="CustomCapabilities" type="CT_CustomCapabilities" />

  <xs:complexType name="CT_CustomCapabilities">
    <xs:sequence>
      <xs:element ref="CustomCapability" minOccurs="1" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>

  <xs:element name="CustomCapability">
    <xs:complexType>
      <xs:attribute name="Name" type="ST_CustomCapability" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:simpleType name="ST_NonEmptyString">
    <xs:restriction base="xs:string">
      <xs:minLength value="1"/>
      <xs:maxLength value="32767"/>
      <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="ST_CustomCapability">
    <xs:annotation>
      <xs:documentation>Custom capabilities should be a string in the form of Company.capabilityName_PublisherId</xs:documentation>
    </xs:annotation>
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Za-z0-9][-_.A-Za-z0-9]*_[a-hjkmnp-z0-9]{13}"/>
      <xs:minLength value="15"/>
      <xs:maxLength value="255"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="AuthorizedEntities" type="CT_AuthorizedEntities" />

  <xs:complexType name="CT_AuthorizedEntities">
    <xs:sequence>
      <xs:element ref="AuthorizedEntity" minOccurs="0" maxOccurs="unbounded"/>
    </xs:sequence>
    <xs:attribute name="AllowAny" type="xs:boolean" use="optional"/>
  </xs:complexType>
  
  <xs:element name="AuthorizedEntity" type="CT_AuthorizedEntity" />
  
  <xs:complexType name="CT_AuthorizedEntity">
    <xs:attribute name="CertificateSignatureHash" type="ST_CertificateSignatureHash" use="required"/>
    <xs:attribute name="AppPackageFamilyName" type="ST_NonEmptyString" use="required"/>
  </xs:complexType>

  <xs:simpleType name="ST_CertificateSignatureHash">
    <xs:restriction base="ST_NonEmptyString">
      <xs:pattern value="[A-Fa-f0-9]+"/>
      <xs:minLength value="64"/>
      <xs:maxLength value="64"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="DeveloperModeOnly">
    <xs:complexType>
      <xs:attribute name="Value" type="xs:boolean" use="required"/>
    </xs:complexType>
  </xs:element>

  <xs:element name="Catalog" type="ST_Catalog" />

  <xs:simpleType name="ST_Catalog">
    <xs:restriction base="xs:string">
      <xs:pattern value="[A-Za-z0-9\+\/\=]+"/>
      <xs:minLength value="4"/>
    </xs:restriction>
  </xs:simpleType>
  
</xs:schema>
```
