---
title: 提交批量元数据包
description: 提交批量元数据包
ms.assetid: c8e248d4-a419-48e1-839d-1bbb9adda382
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 234f587de393dad428b14041e3d25a55e56979cf
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63334920"
---
# <a name="submit-a-bulk-metadata-package"></a>提交批量元数据包


## <a name="span-idsubmittingabulkmetadatapackagespanspan-idsubmittingabulkmetadatapackagespanspan-idsubmittingabulkmetadatapackagespansubmitting-a-bulk-metadata-package"></a><span id="Submitting_a_bulk_metadata_package"></span><span id="submitting_a_bulk_metadata_package"></span><span id="SUBMITTING_A_BULK_METADATA_PACKAGE"></span>提交批量元数据包


**提交批量元数据包**

1.  使用 [SignTool](https://go.microsoft.com/fwlink/p/?LinkId=238330) 工具对批量元数据包进行签名。

2.  从硬件开发人员中心或 Windows 开发人员中心，使用 Microsoft 帐户登录到“仪表板”  。

3.  在“设备元数据”  下，单击“创建批量提交”  。

4.  浏览并选择你的新批量元数据包，然后单击“提交”  。

## <a name="span-idcreatingabulksubmissionpackagespanspan-idcreatingabulksubmissionpackagespanspan-idcreatingabulksubmissionpackagespancreating-a-bulk-submission-package"></a><span id="Creating_a_Bulk_Submission_Package"></span><span id="creating_a_bulk_submission_package"></span><span id="CREATING_A_BULK_SUBMISSION_PACKAGE"></span>创建批量提交程序包


批量元数据提交包是可以将多个设备元数据包提交到仪表板的包格式。

应使用批量提交功能将批量元数据提交包上载到仪表板。 此功能将移除用于创建体验的用户界面，以便简化同时上载多个元数据包的操作。 用于创建体验和修改包属性的信息包含在 BulkMetadataSubmission XML 文档中。

最多可将 50 个 devicemetadata-ms 或 devicemanifest-ms 文件包含在批量程序包中。

有关如何使用“设备元数据提交向导”创建批量元数据包的信息，请参阅[在 Visual Studio 中创建设备元数据提交程序包](https://go.microsoft.com/fwlink/p/?LinkId=251705)。

### <a name="span-idbulkmetadatasubmissionpackagecontentsspanspan-idbulkmetadatasubmissionpackagecontentsspanspan-idbulkmetadatasubmissionpackagecontentsspanbulk-metadata-submission-package-contents"></a><span id="Bulk_Metadata_Submission_Package_Contents"></span><span id="bulk_metadata_submission_package_contents"></span><span id="BULK_METADATA_SUBMISSION_PACKAGE_CONTENTS"></span>批量元数据提交程序包内容

每个批量元数据提交包都包含以下组成部分：

-   设备元数据包

    设备元数据包包含用于显示设备图标，设置操作及使用设备体验功能的信息和图片。

-   设备清单包

    设备清单包包含用于验证设备元数据包的信息。

-   BulkMetadataSubmission XML 文档

    此文档包含用于在没有用户界面情况下正确提交程序包的数据。 仪表板使用此文档中的信息来创建具有友好名称的体验，将程序包组织到体验中、更新体验，以及将各个包标记为预览。

**注意**  这些 XML 文档必须使用 UTF-8 编码进行保存。

在批量元数据提交包中，必须至少包含一个设备元数据或设备清单包。

 

### <a name="span-idstructureofabulkmetadatasubmissionpackagespanspan-idstructureofabulkmetadatasubmissionpackagespanspan-idstructureofabulkmetadatasubmissionpackagespanstructure-of-a-bulk-metadata-submission-package"></a><span id="Structure_of_a_Bulk_Metadata_Submission_Package"></span><span id="structure_of_a_bulk_metadata_submission_package"></span><span id="STRUCTURE_OF_A_BULK_METADATA_SUBMISSION_PACKAGE"></span>批量元数据提交程序包的结构

批量元数据提交包的组成部分存储在压缩的 Cab 文件中。 该文件名必须具有后缀 .bulkmetadata-ms。

每个批量元数据提交包都必须具有以下结构：

``` syntax
DDMMYYYY.bulkmetadata-ms
\Filename1.devicemetadata-ms
\Filename2.devicemetadata-ms
\...
\Filename3.devicemanifest-ms
\Filename4.devicemanifest-ms
\...
\BulkMetadataSubmission.xml
```

Filename1、Filename2、Filename3、Filename4 等必须是 GUID。

若要创建 BulkMetadataSubmission.xml，请参阅下面的信息。

若要开发设备元数据包 \*.devicemetadata-ms，请参阅 [Windows 8 的设备元数据包架构参考](https://go.microsoft.com/fwlink/p/?LinkId=226753)。

若要开发设备清单包 \*.devicemanifest-ms，请参阅[提交电脑设备清单包](https://msdn.microsoft.com/library/windows/hardware/hh801890.aspx)。

你可以使用 Cabarc 工具创建这些 CAB 程序包。 若要了解有关此工具的详细信息，请参阅 [Cabarc 概述](https://go.microsoft.com/fwlink/p/?LinkId=248843)。

使用 Cabarc 工具创建 \*.bulkmetadata-ms 文件时，必须创建一个本地目录，其中设备元数据包 (\*.devicemetadata-ms)、设备清单包 (\*.devicemanifest-ms) 和 BulkMetadataSubmission XML 文档都位于该目录的根目录中。

**备注**

-   .devicemetadata-ms 和 .devicemanifest-ms 文件名必须指定不带花括号 ({}) 分隔符的 GUID。

-   每个设备元数据包和设备清单包的 GUID 都必须唯一。 当你创建新的或修改的程序包时，必须创建新 GUID。

-   有关如何创建 cabinet 文件的更多详细信息，请参阅 [Microsoft Cab SDK](https://go.microsoft.com/fwlink/p/?LinkId=248844)。

**示例**

下面是如何使用 Cabarc 工具创建 .bulkmetadata-ms 文件的示例。 在此示例中，批量元数据文件的组成部分位于名为 BulkPackages 的本地目录中：

``` syntax
.\BulkPackages\
.\BulkPackages\BulkMetadataSubmission.xml
.\BulkPackages\GUID1.devicemetadata-ms
.\BulkPackages\GUID2.devicemetadata-ms
.\BulkPackages\GUID3.devicemanifest-ms
.\BulkPackages\GUID4.devicemanifest-ms
```

GUID.pcmetadata-ms 文件在名为 PCFiles 的本地目录中创建：

``` syntax
Cabarc.exe -r -p -P  .\BulkPackages\ 
N .\BulkFiles\ DDMMYYYY.bulkmetadata-ms 
.\BulkPackages\BulkMetadataSubmission.xml
.\BulkPackages\GUID1.devicemetadata-ms
.\BulkPackages\GUID2.devicemetadata-ms
.\BulkPackages\GUID3.devicemanifest-ms
.\BulkPackages\GUID4.devicemanifest-ms
```

**注意**  有关此工具的详细信息，请参阅 [Cabarc 概述](https://go.microsoft.com/fwlink/p/?LinkId=248843)。

 

## <a name="span-idcreatingbulkmetadatasubmissionxmlspanspan-idcreatingbulkmetadatasubmissionxmlspancreating-bulkmetadatasubmissionxml"></a><span id="creating_bulkmetadatasubmission.xml"></span><span id="CREATING_BULKMETADATASUBMISSION.XML"></span>创建 BulkMetadataSubmission.xml


### <a name="span-idbulkmetadatasubmissionxmlschemaspanspan-idbulkmetadatasubmissionxmlschemaspanspan-idbulkmetadatasubmissionxmlschemaspanbulkmetadatasubmission-xml-schema"></a><span id="BulkMetadataSubmission_XML_Schema"></span><span id="bulkmetadatasubmission_xml_schema"></span><span id="BULKMETADATASUBMISSION_XML_SCHEMA"></span>BulkMetadataSubmission XML 架构

批量元数据提交包包含一个 BulkMetadataSubmission.xml 文档，其中包含仪表板用于创建具有友好名称的体验，将包组织到体验中，更新体验以及将各个包标记为预览的信息。

BulkMetadataSubmission.xml 文档中的数据基于 BulkMetadataSubmission XML 架构（将在下面进行介绍）设置格式。

**注意**  该 XML 文档必须使用 UTF-8 编码进行保存。

 

**BulkMetadataSubmission XML 架构命名空间**

以下是 PcMetadataSubmission XML 架构的命名空间： http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission

**BulkMetadataSubmission XML 元素/属性概述**

下表描述 BulkMetadataSubmission XML 架构的元数据元素和属性。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>元素/属性</th>
<th>元素/属性类型</th>
<th>必需/可选</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>体验</p></td>
<td><p>ExperienceType</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>ExperienceName</p></td>
<td><p>xs:string</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>ExperienceId</p></td>
<td><p>tns:GUIDType</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p>PackageList</p></td>
<td><p>tns:PackageListType</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>PackageFileName</p></td>
<td><p>PackageFileNameType</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>preview</p></td>
<td><p>xs:Boolean</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>locale</p></td>
<td><p>xs:string</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Qualification</p></td>
<td><p>tns:QualificationType</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>LogoSubmissionIDList</p></td>
<td><p>tns:LogoSubmissionIDListType</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p>LogoSubmissionID</p></td>
<td><p>xs:integer</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>更新</p></td>
<td><p>xs:Boolean</p></td>
<td><p>必需</p></td>
</tr>
</tbody>
</table>

 

**BulkMetadataSubmission XML 架构元数据**

以下是 BulkMetadataSubmission XML 架构元数据：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission" xmlns:tns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

 <xs:element name="BulkMetadataSubmission" type="tns:BulkMetadataSubmissionType" />

 <xs:complexType name="BulkMetadataSubmissionType">
  <xs:sequence>
   <xs:element name="Experience" type="tns:ExperienceType"  maxOccurs="unbounded" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

  <xs:complexType name="ExperienceType">
    <xs:complexContent>
      <xs:extension base ="tns:BaseExperienceType">
        <xs:attribute name="update" type="xs:boolean" use="required"/>        
      </xs:extension>      
    </xs:complexContent>
  </xs:complexType>
    
  <xs:complexType name="BaseExperienceType">  
    <xs:sequence>
      <xs:element name="ExperienceName" type="xs:string" />
      <xs:element name="ExperienceId" type="tns:GUIDType" minOccurs="0" />
      <xs:element name="PackageList" type="tns:PackageListType" />
      <xs:element name="Qualification" type="tns:QualificationType" />
      <xs:element name="LogoSubmissionIDList" type="tns:LogoSubmissionIDListType" minOccurs="0" maxOccurs="unbounded" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:simpleType name="GUIDType">
    <xs:restriction base="xs:string">
      <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
    </xs:restriction>
  </xs:simpleType>

 <xs:complexType name="PackageListType">
  <xs:sequence>
   <xs:element name="PackageFileName" type="tns:PackageFileNameType"  maxOccurs="unbounded" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

  <xs:complexType name="PackageFileNameType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="preview" type="xs:boolean" use="required" />
        <xs:attribute name="locale" type="xs:string" use="required" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>

 <xs:simpleType name="QualificationType">
<xs:union memberTypes="tns:QualificationTypeEnumeration xs:string" />
 </xs:simpleType>

 <xs:simpleType name="QualificationTypeEnumeration">
   <xs:restriction base="xs:string">
     <xs:enumeration value="Logo/IDDA" />
     <xs:enumeration value="MicrosoftInboxDriver" />
   </xs:restriction>
 </xs:simpleType>

 <xs:complexType name="LogoSubmissionIDListType">
  <xs:sequence>
   <xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

</xs:schema>
```

### <a name="span-idbulkmetadatasubmissionxmlschemareferencespanspan-idbulkmetadatasubmissionxmlschemareferencespanspan-idbulkmetadatasubmissionxmlschemareferencespanbulkmetadatasubmission-xml-schema-reference"></a><span id="BulkMetadataSubmission_XML_Schema_Reference"></span><span id="bulkmetadatasubmission_xml_schema_reference"></span><span id="BULKMETADATASUBMISSION_XML_SCHEMA_REFERENCE"></span>BulkMetadataSubmission XML 架构参考

BulkMetadataSubmission XML 架构定义以下元素和属性：

-   BulkMetadataSubmission

    -   体验

        -   ExperienceName

        -   ExperienceID

        -   PackageList

            -   PackageFileName

                -   preview

                -   locale

        -   Qualification

        -   LogoSubmissionIDList

            -   LogoSubmissionID

        -   更新

**Experience 元素**

Experience 元素指定单个体验的信息。 有关体验的详细信息，请参阅 [Windows 8 的设备元数据包架构参考](https://go.microsoft.com/fwlink/p/?LinkId=226753)。

仪表板将基于此信息创建具有正确信息的体验并向此体验提交包，或者使用新包更新现有体验。

``` syntax
<xs:element name="Experience" type="tns:ExperienceType"  maxOccurs="unbounded" />

<xs:complexType name="ExperienceType">
  <xs:complexContent>
    <xs:extension base ="tns:BaseExperienceType">
      <xs:attribute name="update" type="xs:boolean" use="required"/>        
    </xs:extension>      
  </xs:complexContent>
</xs:complexType>
    
<xs:complexType name="BaseExperienceType">  
  <xs:sequence>
    <xs:element name="ExperienceName" type="xs:string" />
    <xs:element name="ExperienceId" type="tns:GUIDType" minOccurs="0" />
    <xs:element name="PackageList" type="tns:PackageListType" />
    <xs:element name="Qualification" type="tns:QualificationType" />
    <xs:element name="LogoSubmissionIDList" type="tns:LogoSubmissionIDListType" minOccurs="0" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

备注

可以使用多个 Experience 元素指定多个体验。 这允许一次为不同设备提交许多包。

例如，请参阅下列内容：

``` syntax
<Experience update="false">
  <ExperienceName>Test1</ExperienceName>
  <PackageList>
    <PackageFileName locale="en-us" preview ="false">
      XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemanifest-ms
    </PackageFileName>
  </PackageList>
  <Qualification>Logo/IDDA</Qualification>
  <LogoSubmissionIDList>
    <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
  </LogoSubmissionIDList>
</Experience>

<Experience update="false">
  <ExperienceName>Test2</ExperienceName>
  <PackageList>
    <PackageFileName locale="en-us" preview ="false">
      XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
    </PackageFileName>
  </PackageList>
  <Qualification>Logo/IDDA</Qualification>
  <LogoSubmissionIDList>
    <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
  </LogoSubmissionIDList>
</Experience>
```

**ExperienceName 元素**

ExperienceName 元素指定体验的名称。 如果这是新体验，仪表板将创建具有此名称的体验。 或者，如果这是对现有体验的更新，它将忽略此值。

``` syntax
<xs:element name="ExperienceName" type="xs:string" />
```

**ExperienceId 元素**

ExperienceId 元素指定作为体验 ID 的 GUID。 在更新现有体验时需要使用此值。 仪表板使用此值来标识要更新的体验。

``` syntax
<xs:element name="ExperienceId" type="tns:GUIDType" minOccurs="0" />

<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

**PackageList 元素**

PackageList 元素指定要包含在某个体验中的设备元数据或设备清单包列表。 仪表板使用此信息将这些包添加到新的或现有的体验中。

``` syntax
<xs:element name="PackageList" type="tns:PackageListType" />

<xs:complexType name="PackageListType">
  <xs:sequence>
    <xs:element name="PackageFileName" type="tns:PackageFileNameType"  maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

**PackageFileName 元素**

PackageFileName 元素指定单个设备元数据或设备清单包的文件名和信息。 仪表板使用此信息将程序包添加到新的或现有的体验中，并将该程序包正确标记为预览（如果已指示）。 根据预览值和区域设置值，仪表板也会根据需要删除现有程序包

``` syntax
<xs:element name="PackageFileName" type="tns:PackageFileNameType"  maxOccurs="unbounded" />

<xs:complexType name="PackageFileNameType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="preview" type="xs:boolean" use="required" />
      <xs:attribute name="locale" type="xs:string" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

备注

通过 PackageFileName 元素的 preview 和 locale 属性，仪表板可以使用新提交的包更新你的现有实时包。

例如，如果体验中已存在 en-US 预览包，并且在批量元数据提交程序包中为同一体验提交了 en-US 预览包，则会自动删除现有程序包并提交新程序包。

为此，在更新包时也请务必小心，以避免意外删除。

**preview 属性**

preview 属性指定是否应将设备元数据或设备清单包标记为预览。 有关仪表板如何使用此值的详细信息，请参阅“PackageFileName 元素”。

``` syntax
<xs:attribute name="preview" type="xs:boolean" use="required" />
```

**locale 属性**

locale 属性指定是否应将设备元数据或设备清单包的已声明区域设置（从 PackageInfo.xml）标记为预览。 有关仪表板如何使用此值的详细信息，请参阅“PackageFileName 元素”。

``` syntax
<xs:attribute name="locale" type="xs:string" use="required" />
```

**Qualification 元素**

Qualification 元素指定设备是具有包含在内置驱动程序分发协议 (IDDA) 列表中的徽标认证还是使用 Microsoft 内置驱动程序。 仪表板使用此信息来确保你提交的设备元数据类型的正确设备认证。

``` syntax
<xs:element name="Qualification" type="tns:QualificationType" />

<xs:simpleType name="QualificationType">
<xs:union memberTypes="tns:QualificationTypeEnumeration xs:string" />
 </xs:simpleType>

 <xs:simpleType name="QualificationTypeEnumeration">
   <xs:restriction base="xs:string">
     <xs:enumeration value="Logo/IDDA" />
     <xs:enumeration value="MicrosoftInboxDriver" />
   </xs:restriction>
 </xs:simpleType>
```

**备注**

对于尚未通过徽标认证和未处于 IDDA 列表上的设备，无法使用 Device Stage 这样的功能。

你可以为每个体验选择一个或两个选项。 这些选项及其定义如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>枚举值</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>徽标/IDDA</p></td>
<td><p>你的设备已徽标认证或已在 IDDA 列表上。 如果你已徽标认证，你需要在 LogoSubmissionIDList 元素中指定特定的徽标提交 ID。</p></td>
</tr>
<tr class="even">
<td><p>MicrosoftInboxDrive</p></td>
<td><p>你的设备使用 Microsoft 内置驱动程序。 在使用此资格级别时，设备元数据的某些功能可能无法使用（例如 Device Stage）</p></td>
</tr>
</tbody>
</table>

 

**LogoSubmissionIDList 元素**

LogoSubmissionIDList 元素指定设备的徽标认证列表。 有关仪表板如何使用此值的详细信息，请参阅 Qualification 元素。

``` syntax
<xs:element name="LogoSubmissionIDList" type="tns:LogoSubmissionIDListType" minOccurs="0" maxOccurs="unbounded" />

<xs:complexType name="LogoSubmissionIDListType">
  <xs:sequence>
    <xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

**LogoSubmissionID 元素**

LogoSubmissionID 元素指定设备的单个徽标认证。 有关仪表板如何使用此值的详细信息，请参阅 Qualification 元素。

``` syntax
<xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
```

备注

可以使用多个 LogoSubmissionID 元素为单台设备指示多个徽标认证。 用户应该在列表中为其设备列出所有徽标认证。 下面是列出多个徽标认证的一个示例：

``` syntax
<LogoSubmissionIDList>
  <LogoSubmissionID>0000001</LogoSubmissionID>
  <LogoSubmissionID>0000002</LogoSubmissionID>
  <LogoSubmissionID>0000003</LogoSubmissionID>
</LogoSubmissionIDList>
```

**update 属性**

update 属性指定是否更新某个体验。 仪表板使用此值来更新体验，当 update 属性设置为 true 时，删除发生冲突的包并上载新包。 当 update 属性设置为 false 时，仪表板将创建新体验并向其中上载新包。

``` syntax
<xs:attribute name="update" type="xs:boolean" use="required"/>
```

### <a name="span-idbulkmetadatasubmissionxmlexamplespanspan-idbulkmetadatasubmissionxmlexamplespanspan-idbulkmetadatasubmissionxmlexamplespanbulkmetadatasubmission-xml-example"></a><span id="BulkMetadataSubmission_XML_Example"></span><span id="bulkmetadatasubmission_xml_example"></span><span id="BULKMETADATASUBMISSION_XML_EXAMPLE"></span>BulkMetadataSubmission XML 示例

以下 XML 文档使用 BulkMetadataSubmission XML 架构来指定 BulkMetadataSubmission XML 文档的组成部分。

``` syntax
<BulkMetadataSubmission xmlns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission">

  <Experience update="false">
    <ExperienceName>Test1</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview ="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemanifest-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test2</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview ="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test3</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemanifest-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test4</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

  <Experience update="false">
    <ExperienceName>Test5</ExperienceName>
    <PackageList>
      <PackageFileName locale="en-us" preview="false">
        XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.devicemetadata-ms
      </PackageFileName>
    </PackageList>
    <Qualification>Logo/IDDA</Qualification>
    <LogoSubmissionIDList>
      <LogoSubmissionID>XXXXXXX</LogoSubmissionID>
    </LogoSubmissionIDList>
  </Experience>

</BulkMetadataSubmission>
```

 

 





