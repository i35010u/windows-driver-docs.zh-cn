---
title: 提交电脑设备清单包
description: 提交电脑设备清单包
ms.assetid: b96b02b8-8804-403e-9513-7a5d1b730fcd
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 147d3c944141cbcc8075f7ab2d47193d599ba2ee
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "75209160"
---
# <a name="submit-a-pc-device-manifest-package"></a>提交电脑设备清单包


## <a name="span-idsubmitting_a_pc_device_manifest_packagespanspan-idsubmitting_a_pc_device_manifest_packagespanspan-idsubmitting_a_pc_device_manifest_packagespansubmitting-a-pc-device-manifest-package"></a><span id="Submitting_a_PC_device_manifest_package"></span><span id="submitting_a_pc_device_manifest_package"></span><span id="SUBMITTING_A_PC_DEVICE_MANIFEST_PACKAGE"></span>提交电脑设备清单包


你可以使用相同的方法提交用于预览或发布的包。

**提交设备清单包**

1.  使用 [SignTool](https://go.microsoft.com/fwlink/p/?LinkId=238330) 工具对 devicemanifest-ms 程序包进行签名。

2.  从硬件开发人员中心或 Windows 开发人员中心，使用 Microsoft 帐户登录到“仪表板”  。

3.  在“设备元数据”  下，单击“创建体验”  （如果你希望提交新体验），或单击“管理体验”  （如果你希望修改现有体验）。

4.  浏览并选择你的新 devicemanifest-ms 程序包，然后单击“提交”  。

## <a name="span-idcreating_a_device_manifest_submission_packagespanspan-idcreating_a_device_manifest_submission_packagespanspan-idcreating_a_device_manifest_submission_packagespancreating-a-device-manifest-submission-package"></a><span id="Creating_a_Device_Manifest_Submission_Package"></span><span id="creating_a_device_manifest_submission_package"></span><span id="CREATING_A_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>创建设备清单提交程序包


设备清单提交程序包是所有电脑设备元数据包提交到硬件开发人员中心时必须采用的格式。

设备清单提交程序包包含声明区域设置支持和能够验证电脑 HWID 属于正在进行提交公司的文件。 设备清单包还包含设备元数据包。

设备清单提交程序包采用与设备元数据包相同的方式上载到硬件开发人员中心。 使用相同的用户界面和上传框，输入要上传的 \*.devicemanifest-ms 文件的名称。

硬件开发人员中心用户界面上批量上载以外的所有文件上载框都将接受设备清单提交程序包。

### <a name="span-iddevice_manifest_submission_package_contentsspanspan-iddevice_manifest_submission_package_contentsspanspan-iddevice_manifest_submission_package_contentsspandevice-manifest-submission-package-contents"></a><span id="Device_Manifest_Submission_Package_Contents"></span><span id="device_manifest_submission_package_contents"></span><span id="DEVICE_MANIFEST_SUBMISSION_PACKAGE_CONTENTS"></span>设备清单提交程序包内容

每个设备清单提交包都包含以下组成部分：

-   **设备元数据包**

    此包包含用于在 Windows 中显示设备图标、设置操作及使用设备体验功能的信息和图片。

    设备元数据包始终必需。

-   **LocaleInfo XML 文档**

    此文档包含有关包含在附带设备元数据包中的区域设置的数据。 硬件开发人员中心使用此数据来正确验证一个或多个区域设置的设备元数据包。

    LocaleInfo XML 文档始终是必需的，即使设备元数据包仅包含单个区域设置。

-   **PcMetadataSubmission XML 文档**

    此文档包含用于验证附带的电脑设备元数据包中的 HWID 的数据。 硬件开发人员中心使用此数据来验证设备元数据包中的 HWID 是否属于正确的公司。

    PcMetadataSubmission XML 文档仅对电脑设备元数据包是必需的。

**注意**  这些 XML 文档必须使用 UTF-8 编码进行保存。

 

### <a name="span-idstructure_of_a_pc_device_manifest_submission_packagespanspan-idstructure_of_a_pc_device_manifest_submission_packagespanspan-idstructure_of_a_pc_device_manifest_submission_packagespanstructure-of-a-pc-device-manifest-submission-package"></a><span id="Structure_of_a_PC_Device_Manifest_Submission_Package"></span><span id="structure_of_a_pc_device_manifest_submission_package"></span><span id="STRUCTURE_OF_A_PC_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>电脑设备清单提交包的结构

设备清单包的结构取决于包含的设备元数据用于电脑、用于移动宽带还是包含对多个区域设置的支持。

如果设备元数据不属于这三个类别中的任何一个，则不需要设备清单包。 但是，设备清单包仍然可用于指示设备元数据包是用于单个区域设置的。

电脑设备清单提交包的组成部分存储在压缩的 Cab 文件中。 该文件名必须具有后缀 .devicemanifest-ms。

每个电脑设备清单提交包都必须具有以下结构：

``` syntax
GUID1.devicemanifest-ms
  \GUID1.devicemetadata-ms
  \LocaleInfo.xml
  \PcMetadataSubmission.xml
```

“GUID1”必须是一个 GUID。

若要创建 LocaleInfo.xml 和 PcMetadataSubmission.xml，请参阅以下内容。

若要了解如何开发设备元数据包 \*.devicemetadata-ms，请参阅 [Windows 8 的设备元数据包架构参考](https://go.microsoft.com/fwlink/p/?LinkId=226753)

你可以使用 Cabarc 工具创建这些 CAB 程序包。 有关此工具的详细信息，请参阅 [Cabarc 概述](https://go.microsoft.com/fwlink/p/?LinkId=248843)

使用 Cabarc 工具创建 \*.devicemanifest-ms 文件时，必须创建一个本地目录，其中设备元数据包 (\*.devicemetadata-ms)、LocaleInfo XML 文档和 PcMetadataSubmission XML 文档位于该目录的根目录中。

**备注**

-   .devicemanifest-ms 和 .devicemetadata-ms 文件名必须指定不带花括号 ({}) 分隔符的 GUID。

-   每个电脑设备清单提交和设备元数据包的 GUID 都必须唯一。 当你创建新的或修改的程序包时，必须创建新 GUID。

-   有关如何创建 cabinet 文件的详细信息，请参阅 [Microsoft Cabinet 软件开发工具包](https://go.microsoft.com/fwlink/p/?LinkId=248844)。

**示例**

下面显示了如何使用 Cabarc 工具创建 .devicemanifest-ms 文件的示例。 在此示例中，电脑设备清单文件的组成部分位于名为 PcPackages 的本地目录中：

``` syntax
.\PcPackages\
.\PcPackages\PcMetadataSubmission.xml
.\PcPackages\LocaleInfo.xml
.\PcPackages\GUID.devicemetadata-ms
```

GUID.devicemanifest-ms 文件在名为 PCFiles 的本地目录中创建：

``` syntax
Cabarc.exe -r -p -P  .\PcPackages\ 
N .\PCFiles\ GUID.devicemanifest-ms 
.\PcPackages\PcMetadataSubmission.xml
.\PcPackages\LocaleInfo.xml
```

有关此工具的详细信息，请参阅 [Cabarc 概述](https://go.microsoft.com/fwlink/p/?LinkId=248843)。

## <a name="span-idcreating_pcmetadatasubmissionxmlspanspan-idcreating_pcmetadatasubmissionxmlspancreating-pcmetadatasubmissionxml"></a><span id="creating_pcmetadatasubmission.xml"></span><span id="CREATING_PCMETADATASUBMISSION.XML"></span>创建 PcMetadataSubmission.xml


### <a name="span-idpcmetadatasubmission_xml_schemaspanspan-idpcmetadatasubmission_xml_schemaspanspan-idpcmetadatasubmission_xml_schemaspanpcmetadatasubmission-xml-schema"></a><span id="PcMetadataSubmission_XML_Schema"></span><span id="pcmetadatasubmission_xml_schema"></span><span id="PCMETADATASUBMISSION_XML_SCHEMA"></span>PcMetadataSubmission XML 架构

设备清单提交程序包可包含一个 PcMetadataSubmission.xml 文档，其中包含硬件开发人员中心站点用于验证 PackageInfo.xml 中的计算机硬件 ID 的信息。

PcMetadataSubmission.xml 文档中的数据基于 PcMetadataSubmission XML 架构（将在下面进行介绍）设置格式。

**注意**  该 XML 文档必须使用 UTF-8 编码进行保存。

 

有关 ComputerHardwareID 的详细信息，请参阅[如何创建设备和打印机的设备元数据包](https://go.microsoft.com/fwlink/p/?LinkId=253559)。

**PcMetadataSubmission XML 架构命名空间**

以下是 PcMetadataSubmission XML 架构的命名空间：

-   `http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission`

-   `http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2`

**PcMetadataSubmission XML 元素/属性概述**

下表描述 PcMetadataSubmission XML 架构的元数据元素和属性。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>元素/属性</th>
<th>元素/属性类型</th>
<th>必需/可选</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SMBIOSEntry</p></td>
<td><p>SMBIOSEntryType</p></td>
<td><p>必需</p></td>
<td><p>指定计算机的 SMBIOS 信息。</p></td>
</tr>
<tr class="even">
<td><p>SystemManufacturer</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>必需</p></td>
<td><p>指定计算机的名称。</p></td>
</tr>
<tr class="odd">
<td><p>SystemFamily</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>可选</p></td>
<td><p>指定计算机制造商的系列名称。</p></td>
</tr>
<tr class="even">
<td><p>SystemProductName</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>可选</p></td>
<td><p>指定产品（计算机）的名称。</p></td>
</tr>
<tr class="odd">
<td><p>BIOSVendor</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>可选</p></td>
<td><p>指定 BIOS 制造商的名称。</p></td>
</tr>
<tr class="even">
<td><p>BIOSVersion</p></td>
<td><p>tns:SMBIOSStringType</p></td>
<td><p>可选</p></td>
<td><p>指定 BIOS 的版本号。</p></td>
</tr>
<tr class="odd">
<td><p>SystemBIOSMajorRelease</p></td>
<td><p>tns:BIOSReleaseType</p></td>
<td><p>可选</p></td>
<td><p>指定 BIOS 的 MajorRelease 版本。</p></td>
</tr>
<tr class="even">
<td><p>SystemBIOSMinorRelease</p></td>
<td><p>tns:BIOSReleaseType</p></td>
<td><p>可选</p></td>
<td><p>指定 BIOS 的 MinorRelease 版本。</p></td>
</tr>
<tr class="odd">
<td><p>Enclosuretype</p></td>
<td><p>tns:TypeofEnclosureType</p></td>
<td><p>可选</p></td>
<td><p>指定计算机的机箱类型。</p></td>
</tr>
<tr class="even">
<td><p>SKUNumber</p></td>
<td><p>v2:SMBIOSStringType</p></td>
<td><p>可选</p></td>
<td><p>指定计算机的 SKU 号。</p></td>
</tr>
</tbody>
</table>

 

**PcMetadataSubmission XML 架构定义**

以下是 PcMetadataSubmission XML 架构定义：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission" xmlns:tns="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:v2="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" elementFormDefault="qualified" blockDefault="#all">

  <xs:element name="PcMetadataSubmission" type="tns:PcMetadataSubmissionType" />
  <xs:complexType name="PcMetadataSubmissionType">
    <xs:sequence>
      <xs:element name="SMBIOSList" type="tns:SMBIOSListType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:complexType name="SMBIOSListType">
    <xs:sequence>
      <xs:element name="SMBIOSEntry" type="tns:SMBIOSEntryType" maxOccurs="unbounded" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:complexType name="SMBIOSEntryType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />
        <xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="EnclosureType" type="tns:TypeofEnclosureType" use="optional" />
        <xs:attribute ref="v2:SKUNumber" use="optional" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
  <xs:simpleType name="SMBIOSStringType">
    <xs:restriction base="xs:string">
      <xs:minLength value="1" />
      <xs:maxLength value="64" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="BIOSReleaseType">
    <xs:restriction base="xs:hexBinary">
      <xs:minLength value="1" />
      <xs:maxLength value="1" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="TypeofEnclosureType">
    <xs:restriction base="xs:hexBinary">
      <xs:pattern value="([0-7][0-9A-F]|0[0-9A-F])" />
    </xs:restriction>
  </xs:simpleType>
</xs:schema>
```

以下是 PcMetadataSubmissionv2 XML 架构定义：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" xmlns:tns="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

  <xs:attribute name="SKUNumber" type="tns:SMBIOSStringType" />

  <xs:simpleType name="SMBIOSStringType">
    <xs:restriction base="xs:string">
      <xs:minLength value="1" />
      <xs:maxLength value="64" />
    </xs:restriction>
  </xs:simpleType>

</xs:schema>
```

### <a name="span-idpcmetadatasubmission_xml_schema_referencespanspan-idpcmetadatasubmission_xml_schema_referencespanspan-idpcmetadatasubmission_xml_schema_referencespanpcmetadatasubmission-xml-schema-reference"></a><span id="PcMetadataSubmission_XML_Schema_Reference"></span><span id="pcmetadatasubmission_xml_schema_reference"></span><span id="PCMETADATASUBMISSION_XML_SCHEMA_REFERENCE"></span>PcMetadataSubmission XML 架构参考

PcMetadataSubmission XML 架构定义以下元素和属性：

-   SMBIOSList

    -   SMBIOSEntry

        -   SystemManufacturer

        -   SystemFamily

        -   SystemProductName

        -   BIOSVendor

        -   BIOSVersion

        -   SystemBIOSMajorRelease

        -   SystemBIOSMinorRelease

        -   Enclosuretype

        -   SKUNumber

**SMBIOSEntry 元素**

SMBIOSEntry 元素指定计算机系统信息。 硬件开发人员中心将基于此信息创建计算机硬件 ID，并将该值与你随 PcMetadataSubmission.xml 一起提交的 packageinfo.xml 中的计算机硬件 ID 进行比较。

``` syntax
<xs:element name="SMBIOSEntry" type="tns:SMBIOSEntryType" maxOccurs="unbounded" />

<xs:complexType name="SMBIOSEntryType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />
        <xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="Enclosuretype" type="tns:TypeofEnclosureType" use="optional" />
        <xs:anyAttribute namespace="##other" processContents="lax" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
```

**备注**

可以使用多个 SMBIOSEntry 元素指定多个系统。

例如，考虑元数据包支持多个电脑系统。 可以使用以下 SMBIOSEntry 元素定义电脑系统。

``` syntax
<SMBIOSList>
  <SMBIOSEntry
      SystemManufacturer="FABRIKAM" SystemFamily…
  />
  <SMBIOSEntry
      SystemManufacturer="FABRIKAM" SystemFamily…
</SMBIOSList>
```

**SystemManufacturer 属性**

SystemManufacturer 属性指定计算机的系列名称。

``` syntax
<xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

SystemManufacturer 属性指定的值必须与目标电脑 SMBIOS 表中“制造商”字段中的值相同。 下表显示了 SMBIOS 中“制造商”字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>制造商</p></td>
<td><p>系统信息(类型 1)</p></td>
<td><p>2.0+</p></td>
<td><p>04h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机制造商的名称。</p></td>
</tr>
</tbody>
</table>

 

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**SystemFamily 属性**

SystemFamily 属性指定计算机制造商的名称。

``` syntax
<xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

SystemFamily 属性指定的值必须与目标电脑 SMBIOS 表中“系列”字段中的值相同。 下表显示了 SMBIOS 中“系列”字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>家庭</p></td>
<td><p>系统信息(类型 1)</p></td>
<td><p>2.4+</p></td>
<td><p>1Ah</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定特定计算机所属的系列。系列指从硬件或软件的视角来看相似但不完全相同的一组计算机。通常，一个系列由不同的计算机型号组成，而这些型号具有不同的配置和价格点。 同一系列中的计算机通常具有相似的品牌和外观特点。</p></td>
</tr>
</tbody>
</table>

 

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**SystemProductName 属性**

SystemProductName 属性指定产品（计算机）的名称。

``` syntax
<xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

SystemProductName 属性指定的值必须与目标电脑 SMBIOS 表中“产品名称”字段中的值相同。 下表显示了 SMBIOS 中“产品名称”字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>产品名称</p></td>
<td><p>系统信息(类型 1)</p></td>
<td><p>2.0+</p></td>
<td><p>05h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机的产品名称。</p></td>
</tr>
</tbody>
</table>

 

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**BIOSVendor 属性**

BIOSVendor 属性指定 BIOS 制造商的名称。

``` syntax
<xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

BIOSVendor 属性指定的值必须与目标电脑 SMBIOS 表中“供应商”字段中的值相同。 下表显示了 SMBIOS 中“供应商”字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>供应商</p></td>
<td><p>BIOS 信息(类型 0)</p></td>
<td><p>2.0</p></td>
<td><p>04h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定 BIOS 供应商的名称。</p></td>
</tr>
</tbody>
</table>

 

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**BIOSVersion 属性**

BIOSVersion 属性指定 BIOS 的版本号。

``` syntax
<xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

BIOSVersion 属性指定的值必须与目标电脑 SMBIOS 表中“BIOS 版本”字段中的值相同。 下表显示了 SMBIOS 中“BIOS 版本”字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BIOS 版本</p></td>
<td><p>BIOS 信息(类型 0)</p></td>
<td><p>2.0</p></td>
<td><p>05h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串包含有关处理器核心和 OEM 版本的信息。</p></td>
</tr>
</tbody>
</table>

 

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**SystemBIOSMajorRelease 属性**

SystemBIOSMajorRelease 属性指定 BIOS 的主要发行版本。

``` syntax
<xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />

<xs:simpleType name="BIOSReleaseType">
  <xs:restriction base="xs:hexBinary">
    <xs:minLength value="1" />
    <xs:maxLength value="1" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

SystemBIOSMajorRelease 属性指定的值必须与目标电脑 SMBIOS 表中 SystemBIOSMajorRelease 字段中的值相同。 下表显示了 SMBIOS 中 SystemBIOSMajorRelease 字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>系统 BIOS 主要版本</p></td>
<td><p>BIOS 信息(类型 0)</p></td>
<td><p>2.4</p></td>
<td><p>14h</p></td>
<td><p>BYTE</p></td>
<td><p>视情况而定。</p></td>
<td><p>系统 BIOS 的主要版本。</p></td>
</tr>
</tbody>
</table>

 

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**SystemBIOSMinorRelease 属性**

SystemBIOSMinorRelease 属性指定 BIOS 的次要发行版本。

``` syntax
<xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />

<xs:simpleType name="BIOSReleaseType">
  <xs:restriction base="xs:hexBinary">
    <xs:minLength value="1" />
    <xs:maxLength value="1" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

SystemBIOSMinorRelease 属性指定的值必须与目标电脑 SMBIOS 表中 SystemBIOSMinorRelease 字段中的值相同。 下表显示了 SMBIOS 中 SystemBIOSMinorRelease 字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>系统 BIOS 次要版本</p></td>
<td><p>BIOS 信息(类型 0)</p></td>
<td><p>2.4</p></td>
<td><p>15h</p></td>
<td><p>BYTE</p></td>
<td><p>视情况而定。</p></td>
<td><p>系统 BIOS 的次要版本。</p></td>
</tr>
</tbody>
</table>

 

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**Enclosuretype 属性**

Enclosuretype 属性指定计算机的机箱类型。

``` syntax
<xs:attribute name="EnclosureType" type="tns:TypeofEnclosureType" use="optional" />

<xs:simpleType name="TypeofEnclosureType">
  <xs:restriction base="xs:hexBinary">
    <xs:pattern value="([0-7][0-9A-F]|0[0-9A-F])" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

Enclosuretype 属性指定的值必须与目标电脑 SMBIOS 表中“机箱”字段中的值相同。 下表显示了 SMBIOS 中“机箱”字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>机箱类型</p></td>
<td><p>系统机箱(类型 3)</p></td>
<td><p>2.0+</p></td>
<td><p>05h</p></td>
<td><p>BYTE</p></td>
<td><p>视情况而定。</p></td>
<td><p>系统机箱或机壳类型。</p></td>
</tr>
</tbody>
</table>

 

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

**SKUNumber 元素**

SKUNumber 元素指定计算机的 SKU 号。

``` syntax
<xs:attribute name="SKUNumber" type="tns:SMBIOSStringType" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

**备注**

SKUNumber 元素指定的值必须与目标电脑 SMBIOS 表中“SKU 号”字段中的值相同。 下表显示了 SMBIOS 中“SKU 号”字段的字段信息。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>结构名称和类型</th>
<th>SMBIOS 规范版本</th>
<th>偏移量</th>
<th>长度</th>
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SKU 号</p></td>
<td><p>系统信息(类型 1)</p></td>
<td><p>2.4+</p></td>
<td><p>19h</p></td>
<td><p>BYTE</p></td>
<td><p>STRING</p></td>
<td><p>以 Null 结尾的字符串编号。此文本字符串用于标识销售的特定计算机配置。 有时也将它称为产品 ID 或采购订单号。 此编号通常会在现有字段中找到，但是没有标准格式。 通常，对于给定 OEM 的给定系统板，会有数十个独特的处理器、内存、硬盘驱动器和光驱配置。</p></td>
</tr>
</tbody>
</table>

 

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="span-idpcmetadatasubmission_xml_examplespanspan-idpcmetadatasubmission_xml_examplespanspan-idpcmetadatasubmission_xml_examplespanpcmetadatasubmission-xml-example"></a><span id="PcMetadataSubmission_XML_Example"></span><span id="pcmetadatasubmission_xml_example"></span><span id="PCMETADATASUBMISSION_XML_EXAMPLE"></span>PcMetadataSubmission XML 示例

以下 XML 文档使用 PcMetadataSubmission XML 架构来指定目标计算机的 PcMetadataSubmission 信息的组成部分。

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<PcMetadataSubmission xmlns="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission">
  <SMBIOSList>
   <SMBIOSEntry
      SystemManufacturer="FABRIKAM"
      SystemFamily="FABRIKAM A SERIES"
      SystemProductName="FABRIKAM LAPTOP"
      BIOSVendor="FABRIKAM"
      BIOSVersion="7BETC7WW (2.08 )"
      SystemBIOSMajorRelease="08"
      SystemBIOSMinorRelease="00"
      EnclosureType="0A"
      v2:SKUNumber="1234567890ABCD"
    />
  </SMBIOSList>
</PcMetadataSubmission>
```

## <a name="span-idcreating_localeinfoxmlspanspan-idcreating_localeinfoxmlspancreating-localeinfoxml"></a><span id="creating_localeinfo.xml"></span><span id="CREATING_LOCALEINFO.XML"></span>创建 LocaleInfo.xml


有关创建用于提交的 Localeinfo.xml 文件的信息，请参阅[创建 LocaleInfo.xml 提交文件](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)。

 

 





