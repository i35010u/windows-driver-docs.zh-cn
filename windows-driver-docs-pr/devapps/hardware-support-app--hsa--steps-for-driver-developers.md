---
title: 硬件支持应用 (为驱动程序开发人员) 步骤 HSA
description: '创建自定义功能，将驱动程序与硬件支持应用配对 (HSA) '
keywords:
- 自定义，功能
- UWP 应用
- 自定义功能
- UWP
- 硬件
ms.date: 08/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e849f7c3cc5970c0bfaa9369a5997c078d9617b1
ms.sourcegitcommit: 55a1002032ce9b01c6db26b41eca86a1bcb33c84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2021
ms.locfileid: "98626073"
---
# <a name="hardware-support-app-hsa-steps-for-driver-developers"></a>硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤

硬件支持应用 (HSA) 是设备特定的应用，与特定驱动程序或 [RPC (远程过程调用) ](/windows/desktop/Rpc/rpc-start-page) 终结点配对。

若要将应用商店应用与驱动程序相关联，请首先保留称为 "自定义功能" 的特殊值。 然后，允许访问广告功能并向应用开发人员提供功能的应用。  本页介绍了驱动程序开发人员的这些步骤。

应用开发人员的步骤在硬件支持应用中进行了介绍 [ (HSA) ：适用于应用开发人员的步骤](hardware-support-app--hsa--steps-for-app-developers.md)。

HSA 是 [Windows 驱动程序](../develop/getting-started-with-windows-drivers.md)) 设计原则的三个 ( "DCH" 中的一种。

## <a name="reserving-a-custom-capability"></a>保留自定义功能

首先，保留自定义功能：

1. 电子邮件 Microsoft 硬件支持应用查看 (<HSAReview@microsoft.com>) ，并提供以下信息：

    * 联系信息
    * 公司名称
    * 功能 (的名称必须是唯一的，并引用所有者) 
    * 功能需要访问哪些资源？
    * 任何安全或隐私问题
    * 将向合作伙伴处理哪些数据事件？
      * 这些事件是否包括个人标识符，如精确的用户位置、密码、IP 地址、PUID、设备 ID、CID、用户名和联系人数据) ？
      * 数据事件是停留在用户设备上，还是发送到合作伙伴？
    * 你的功能提供了哪些数据？
    * 此功能的最终用户权益是什么？
    * 包括 Microsoft Store 应用发行者 ID。  若要获取一个，请在 Microsoft Store 页上创建一个主干应用项。 有关保留应用 PFN 的详细信息，请参阅 [通过保留名称创建应用](/windows/uwp/publish/create-your-app-by-reserving-a-name)。

2. 如果批准了请求，Microsoft 将通过电子邮件返回 **capabilityName \_ PublisherID** 格式的唯一自定义功能字符串名称。

现在，你可以使用自定义功能来允许访问 RPC 终结点或驱动程序。

## <a name="allowing-access-to-an-rpc-endpoint-to-a-uwp-app-using-the-custom-capability"></a>允许使用自定义功能访问某个 UWP 应用的 RPC 终结点

若要允许对具有自定义功能的 UWP 应用访问 RPC 终结点，请执行以下步骤：

1. 调用 [**DeriveCapabilitySidsFromName**](/windows/win32/api/securitybaseapi/nf-securitybaseapi-derivecapabilitysidsfromname) ，将自定义功能名称转换为 (SID) 的安全 ID。
2. 将 SID 添加到 access 允许的 ACE 以及 RPC 终结点安全描述符所需的任何其他 Sid。
3. 使用安全描述符中的信息创建 RPC 终结点。

在[自定义功能示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomCapability)的[RPC 服务器代码](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/CustomCapability/Service/Server/RpcServer.cpp)中，可以看到上述的实现。

## <a name="allowing-access-to-a-driver-to-a-uwp-app-using-the-custom-capability"></a>允许使用自定义功能访问 UWP 应用的驱动程序

若要允许使用自定义功能访问 UWP 应用的驱动程序，请在 INF 文件或驱动程序源中添加一些行。

在 INF 文件中指定自定义功能，如下所示：

```cpp
[WDMPNPB003_Device.NT.Interfaces]
AddInterface= {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz},,AddInterfaceSection

[AddInterfaceSection]
AddProperty= AddInterfaceSection.AddProps

[AddInterfaceSection.AddProps]
; DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities
{026e516e-b814-414b-83cd-856d6fef4822}, 8, 0x2012,, "CompanyName.myCustomCapabilityNameTBD_MyStorePubId"
```

或者，在驱动程序中执行以下操作：

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

替换为 `zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz` 要公开的接口的 GUID。  请将 " *myCustomCapabilityNameTBD* *" 替换为* 公司名称，将 "名称" 替换为公司中唯一的名称，并将 " *MyStorePubId* " 替换为你的发布者存储区 ID。

有关上面所示的驱动程序代码示例，请参阅 [适用于通用驱动程序的驱动程序包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)。

若要在内核模式下设置属性，请使用如下所示的代码：

```cpp
#if defined(NTDDI_WIN10_RS2) && (NTDDI_VERSION >= NTDDI_WIN10_RS2)

//
// Adding Custom Capability:
//
// Adds a custom capability to device interface instance that allows a Windows
// Store device app to access this interface using Windows.Devices.Custom namespace.
// This capability can be defined either in INF or here as shown below. In order
// to define it from the INF, uncomment the section "OsrUsb Interface installation"
// from the INF and remove the block of code below.
//

static const wchar_t customCapabilities[] = L"microsoft.hsaTestCustomCapability_q536wpkpf5cy2\0";

status = g_pIoSetDeviceInterfacePropertyData(&symbolicLinkName,
                                              &DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities,
                                              0,
                                              0,
                                              DEVPROP_TYPE_STRING_LIST,
                                              sizeof(customCapabilities),
                                              (PVOID)&customCapabilities);

if (!NT_SUCCESS(status)) {
    TraceEvents(TRACE_LEVEL_ERROR, DBG_PNP,
                "IoSetDeviceInterfacePropertyData failed to set custom capability property  %!STATUS!\n", status);
    goto Error;
}

#endif
```

## <a name="preparing-the-signed-custom-capability-descriptor-sccd-file"></a>准备 (SCCD) 文件的已签名自定义功能描述符

已签名的自定义功能描述符 (SCCD) 文件是一个签名的 XML 文件，授权使用一个或多个自定义功能。  驱动程序或 RPC 终结点的所有者通过提供此文件向应用开发人员授予自定义功能。

若要准备 SCCD 文件，请首先更新自定义功能字符串。  使用以下示例作为起点：

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

接下来，自定义功能所有者将从应用开发人员那里获取包系列名称 (PFN) 和签名哈希，并在 SCCD 文件中更新这些字符串。

>[!NOTE]
>应用无需直接使用证书进行签名，但指定的证书必须是对应用进行签名的证书链的一部分。

完成 SCCD 后，功能所有者会将其通过电子邮件发送给 Microsoft 进行签名。  Microsoft 将向功能所有者返回已签名的 SCCD。

然后，功能所有者将 SCCD 发送到应用开发人员。  应用程序开发人员在应用程序清单中包含已签名的 SCCD。  若要了解应用开发人员需要执行的操作，请参阅 [硬件支持应用 (HSA) ：应用开发人员的步骤](hardware-support-app--hsa--steps-for-app-developers.md)。

## <a name="limiting-the-scope-of-an-sccd"></a>限制 SCCD 的范围

出于测试目的，自定义功能所有者可以限制在开发人员模式下将硬件支持应用安装到计算机。

为此，请在获取由 Microsoft 签署的 SCCD 之前添加 **DeveloperModeOnly**：

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

生成的已签名 SCCD 仅适用于以 [开发人员模式](/windows/uwp/get-started/enable-your-device-for-development)运行的设备。

## <a name="allowing-any-app-to-use-a-custom-capability"></a>允许任何应用使用自定义功能

建议指定可使用自定义功能)  (应用的授权实体。 但是，在某些情况下，你可能希望允许任何应用包括 SCCD。  从 Windows 10 版本1809开始，可以通过将 **AllowAny** 添加到 AuthorizedEntities 元素来实现此目的。 由于最好的做法是在 SCCD 文件中声明授权的实体，因此，请在提交你的 SCCD 以由 Microsoft 签名时，提供使用 **AllowAny** 的理由。

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

生成的已签名 SCCD 将在任何应用包中进行验证。

## <a name="multiple-sccds"></a>多个 SCCDs

从 Windows 10 版本1803开始，应用可声明一个或多个 SCCD 文件中的自定义功能。 将 SCCD 文件放置在应用包的根目录中。

## <a name="summary"></a>总结

下图总结了上述顺序：

![获取已签名的 SCCD](images/signsccd.png)

## <a name="see-also"></a>另请参阅

* [Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)
* [通用 Windows 平台简介](/windows/uwp/get-started/universal-application-platform-guide)
* [通用 Windows 平台 (UWP)](/windows/uwp/design/basics/design-and-ui-intro)
* [应用功能](/windows/uwp/packaging/app-capability-declarations)
* [使用 Visual Studio 开发 UWP 应用](/windows/uwp/develop/)
* [将驱动程序与通用 Windows 平台 (UWP) 应用配对](../install/pairing-app-and-driver-versions.md)
* [开发 UWP 应用](/windows/uwp/develop/)
* [使用 Desktop App Converter 将应用打包（桌面桥）](/windows/uwp/porting/desktop-to-uwp-run-desktop-app-converter)
* [自定义功能示例应用](https://go.microsoft.com/fwlink/p/?LinkId=846904)
* [自定义功能驱动程序示例](https://aka.ms/customcapabilitydriversample )
* [Windows 10 中的旁加载应用](/windows/deploy/sideload-apps-in-windows-10)
* [自定义功能常见问题](FAQ-on-custom-capabilities.md)

## <a name="sccd-xml-schema"></a>SCCD XML 架构

下面是 SCCD 文件的正式 XML XSD 架构。  提交 SCCD 之前，请使用此架构验证你的。  有关导入架构和使用 IntelliSense 进行验证的信息，请参阅 [架构缓存](/visualstudio/xml-tools/schema-cache) 和 [XML 文档验证](/visualstudio/xml-tools/xml-document-validation) 。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
  xmlns:xs="https://www.w3.org/2001/XMLSchema"
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

在 Windows 10 版本1809中，下面的架构也是有效的。  它允许 SCCD 将任何应用包声明为授权实体。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
  xmlns:xs="https://www.w3.org/2001/XMLSchema"
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