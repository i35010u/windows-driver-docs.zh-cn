---
title: 提交批量元数据包
description: 为驱动程序创建批量元数据包的组件 - 设备元数据包、设备清单包和 BulkMetadataSubmission XML 文档。
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dc59049a3e516626648d555c35773eed0d026ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800291"
---
# <a name="submit-a-bulk-metadata-package"></a>提交批量元数据包

提交批量元数据包：

1. 使用 [SignTool](/windows/win32/seccrypto/signtool) 工具对批量元数据包进行签名。

2. 从硬件开发人员中心或 Windows 开发人员中心，使用 Microsoft 帐户登录到“仪表板”。

3. 在“设备元数据”下，单击“创建批量提交”。

4. 浏览并选择你的新批量元数据包，然后单击“提交”。

## <a name="creating-a-bulk-submission-package"></a>创建批量提交程序包

批量元数据提交包是可以将多个设备元数据包提交到仪表板的包格式。

应使用批量提交功能将批量元数据提交包上载到仪表板。 此功能将移除用于创建体验的用户界面，以便简化同时上载多个元数据包的操作。 用于创建体验和修改包属性的信息包含在 BulkMetadataSubmission XML 文档中。

最多可将 50 个 devicemetadata-ms 或 devicemanifest-ms 文件包含在批量程序包中。

有关如何使用“设备元数据提交向导”创建批量元数据包的信息，请参阅[在 Visual Studio 中创建设备元数据提交程序包](../devtest/using-the-submission-tool.md)。

### <a name="bulk-metadata-submission-package-contents"></a>批量元数据提交程序包内容

每个批量元数据提交包都包含以下组成部分：

- 设备元数据包

    设备元数据包包含用于显示设备图标，设置操作及使用设备体验功能的信息和图片。

- 设备清单包

    设备清单包包含用于验证设备元数据包的信息。

- BulkMetadataSubmission XML 文档

    此文档包含用于在没有用户界面情况下正确提交程序包的数据。 仪表板使用此文档中的信息来创建具有友好名称的体验，将程序包组织到体验中、更新体验，以及将各个包标记为预览。

>[!NOTE]
>这些 XML 文档必须使用 UTF-8 编码进行保存。

在批量元数据提交包中，必须至少包含一个设备元数据或设备清单包。

### <a name="structure-of-a-bulk-metadata-submission-package"></a>批量元数据提交包的结构

批量元数据提交包的组成部分存储在压缩的 Cab 文件中。 该文件名必须具有后缀 .bulkmetadata-ms。

每个批量元数据提交包都必须具有以下结构：

```syntax
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

若要创建 BulkMetadataSubmission.xml，请参阅下面的[创建 BulkMetadataSubmission.xml](#creating-bulkmetadatasubmissionxml)。

若要开发设备元数据包 \*.devicemetadata-ms，请参阅 [Windows 8 的设备元数据包架构参考](/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))。

若要开发设备清单包 \*.devicemanifest-ms，请参阅[提交电脑设备清单包](submit-a-pc-device-manifest-package.md)。

你可以使用 Cabarc 工具创建这些 CAB 程序包。 若要了解有关此工具的详细信息，请参阅 [Cabarc 概述](/previous-versions/windows/it-pro/windows-server-2003/cc781787(v=ws.10))。

使用 Cabarc 工具创建 \*.bulkmetadata-ms 文件时，必须创建一个本地目录，其中设备元数据包 (\*.devicemetadata-ms)、设备清单包 (\*.devicemanifest-ms) 和 BulkMetadataSubmission XML 文档都位于该目录的根目录中。

## <a name="remarks"></a>备注

- .devicemetadata-ms 和 .devicemanifest-ms 文件名必须指定不带花括号 ({}) 分隔符的 GUID。

- 每个设备元数据包和设备清单包的 GUID 都必须唯一。 当你创建新的或修改的程序包时，必须创建新 GUID。

- 有关如何创建 cabinet 文件的更多详细信息，请参阅 [Microsoft Cab SDK](/previous-versions/ms974336(v=msdn.10))。

## <a name="example"></a>示例

下面是如何使用 Cabarc 工具创建 .bulkmetadata-ms 文件的示例。 在此示例中，批量元数据文件的组成部分位于名为 BulkPackages 的本地目录中：

```syntax
.\BulkPackages\
.\BulkPackages\BulkMetadataSubmission.xml
.\BulkPackages\GUID1.devicemetadata-ms
.\BulkPackages\GUID2.devicemetadata-ms
.\BulkPackages\GUID3.devicemanifest-ms
.\BulkPackages\GUID4.devicemanifest-ms
```

GUID.pcmetadata-ms 文件在名为 PCFiles 的本地目录中创建：

```syntax
Cabarc.exe -r -p -P  .\BulkPackages\
N .\BulkFiles\ DDMMYYYY.bulkmetadata-ms
.\BulkPackages\BulkMetadataSubmission.xml
.\BulkPackages\GUID1.devicemetadata-ms
.\BulkPackages\GUID2.devicemetadata-ms
.\BulkPackages\GUID3.devicemanifest-ms
.\BulkPackages\GUID4.devicemanifest-ms
```

>[!Note]
>有关此工具的详细信息，请参阅 [Cabarc 概述](/previous-versions/windows/it-pro/windows-server-2003/cc781787(v=ws.10))。

## <a name="creating-bulkmetadatasubmissionxml"></a>创建 BulkMetadataSubmission.xml

### <a name="bulkmetadatasubmission-xml-schema"></a>BulkMetadataSubmission XML 架构

批量元数据提交包包含一个 BulkMetadataSubmission.xml 文档，其中包含仪表板用于创建具有友好名称的体验，将包组织到体验中，更新体验以及将各个包标记为预览的信息。

BulkMetadataSubmission.xml 文档中的数据基于 BulkMetadataSubmission XML 架构（将在下面进行介绍）设置格式。

>[!NOTE]
>该 XML 文档必须使用 UTF-8 编码进行保存。

### <a name="bulkmetadatasubmission-xml-schema-namespace"></a>BulkMetadataSubmission XML 架构命名空间

以下是 PcMetadataSubmission XML 架构的命名空间：`http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/BulkMetadataSubmission`

### <a name="overview-of-bulkmetadatasubmission-xml-elementsattributes"></a>BulkMetadataSubmission XML 元素/属性概述

下表描述 BulkMetadataSubmission XML 架构的元数据元素和属性。

|元素/属性|元素/属性类型|必需/可选|
|----|----|----|
|体验|ExperienceType|必需|
|ExperienceName|xs:string|必需|
|ExperienceId|tns:GUIDType|可选|
|PackageList|tns:PackageListType|必需|
|PackageFileName|PackageFileNameType|必需|
|preview|xs:Boolean|必需|
|locale|xs:string|必需|
|Qualification|tns:QualificationType|必需|
|LogoSubmissionIDList|tns:LogoSubmissionIDListType|可选|
|LogoSubmissionID|xs:integer|必需|
|更新|xs:Boolean|必需|

### <a name="bulkmetadatasubmission-xml-schema-metadata"></a>BulkMetadataSubmission XML 架构元数据

以下是 BulkMetadataSubmission XML 架构元数据：

```syntax
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

### <a name="bulkmetadatasubmission-xml-schema-reference"></a>BulkMetadataSubmission XML 架构参考

BulkMetadataSubmission XML 架构定义以下元素和属性：

- BulkMetadataSubmission

  - 体验

    - ExperienceName

    - ExperienceID

    - PackageList

      - PackageFileName

        - preview

        - locale

    - Qualification

    - LogoSubmissionIDList

      - LogoSubmissionID

    - 更新

### <a name="experience-element"></a>Experience 元素

Experience 元素指定单个体验的信息。 有关体验的详细信息，请参阅 [Windows 8 的设备元数据包架构参考](/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))。

仪表板将基于此信息创建具有正确信息的体验并向此体验提交包，或者使用新包更新现有体验。

```syntax
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

### <a name="experiencename-element"></a>ExperienceName 元素

ExperienceName 元素指定体验的名称。 如果这是新体验，仪表板将创建具有此名称的体验。 或者，如果这是对现有体验的更新，它将忽略此值。

``` syntax
<xs:element name="ExperienceName" type="xs:string" />
```

### <a name="experienceid-element"></a>ExperienceId 元素

ExperienceId 元素指定作为体验 ID 的 GUID。 在更新现有体验时需要使用此值。 仪表板使用此值来标识要更新的体验。

``` syntax
<xs:element name="ExperienceId" type="tns:GUIDType" minOccurs="0" />

<xs:simpleType name="GUIDType">
  <xs:restriction base="xs:string">
    <xs:pattern value="[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}" />
  </xs:restriction>
</xs:simpleType>
```

### <a name="packagelist-element"></a>PackageList 元素

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

### <a name="packagefilename-element"></a>PackageFileName 元素

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

通过 PackageFileName 元素的 preview 和 locale 属性，仪表板可以使用新提交的包更新你的现有实时包。

例如，如果体验中已存在 en-US 预览包，并且在批量元数据提交程序包中为同一体验提交了 en-US 预览包，则会自动删除现有程序包并提交新程序包。

为此，在更新包时也请务必小心，以避免意外删除。

### <a name="preview-attribute"></a>preview 属性

preview 属性指定是否应将设备元数据或设备清单包标记为预览。 有关仪表板如何使用此值的详细信息，请参阅“PackageFileName 元素”。

``` syntax
<xs:attribute name="preview" type="xs:boolean" use="required" />
```

### <a name="locale-attribute"></a>locale 属性

locale 属性指定是否应将设备元数据或设备清单包的已声明区域设置（从 PackageInfo.xml）标记为预览。 有关仪表板如何使用此值的详细信息，请参阅“PackageFileName 元素”。

``` syntax
<xs:attribute name="locale" type="xs:string" use="required" />
```

### <a name="qualification-element"></a>Qualification 元素

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

对于尚未通过徽标认证和未处于 IDDA 列表上的设备，无法使用 Device Stage 这样的功能。

你可以为每个体验选择一个或两个选项。 这些选项及其定义如下表所示。

|枚举值|描述|
|----|----|
|徽标/IDDA|你的设备已徽标认证或已在 IDDA 列表上。 如果你已徽标认证，你需要在 LogoSubmissionIDList 元素中指定特定的徽标提交 ID。|
|MicrosoftInboxDrive|你的设备使用 Microsoft 内置驱动程序。 在使用此资格级别时，设备元数据的某些功能可能无法使用（例如 Device Stage）|

### <a name="logosubmissionidlist-element"></a>LogoSubmissionIDList 元素

LogoSubmissionIDList 元素指定设备的徽标认证列表。 有关仪表板如何使用此值的详细信息，请参阅 Qualification 元素。

```syntax
<xs:element name="LogoSubmissionIDList" type="tns:LogoSubmissionIDListType" minOccurs="0" maxOccurs="unbounded" />

<xs:complexType name="LogoSubmissionIDListType">
  <xs:sequence>
    <xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

### <a name="logosubmissionid-element"></a>LogoSubmissionID 元素

LogoSubmissionID 元素指定设备的单个徽标认证。 有关仪表板如何使用此值的详细信息，请参阅 Qualification 元素。

```syntax
<xs:element name="LogoSubmissionID" type="xs:integer"  maxOccurs="unbounded" />
```

可以使用多个 LogoSubmissionID 元素为单台设备指示多个徽标认证。 用户应该在列表中为其设备列出所有徽标认证。 下面是列出多个徽标认证的一个示例：

```syntax
<LogoSubmissionIDList>
  <LogoSubmissionID>0000001</LogoSubmissionID>
  <LogoSubmissionID>0000002</LogoSubmissionID>
  <LogoSubmissionID>0000003</LogoSubmissionID>
</LogoSubmissionIDList>
```

### <a name="update-attribute"></a>update 属性

update 属性指定是否更新某个体验。 仪表板使用此值来更新体验，当 update 属性设置为 true 时，删除发生冲突的包并上载新包。 当 update 属性设置为 false 时，仪表板将创建新体验并向其中上载新包。

```syntax
<xs:attribute name="update" type="xs:boolean" use="required"/>
```

### <a name="bulkmetadatasubmission-xml-example"></a>BulkMetadataSubmission XML 示例

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
