---
title: 提交多区域设置设备清单包
description: 提交多区域设置设备清单包
ms.assetid: b6748bff-d730-434e-9316-dc7b7222b727
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a458e1d7dab7983d78b6018eef83ea7762fe5176
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518530"
---
# <a name="submit-a-multiple-locale-device-manifest-package"></a>提交多区域设置设备清单包


## <a name="span-idsubmittingamultiple-localedevicemanifestpackagespanspan-idsubmittingamultiple-localedevicemanifestpackagespanspan-idsubmittingamultiple-localedevicemanifestpackagespansubmitting-a-multiple-locale-device-manifest-package"></a><span id="Submitting_a_multiple-locale_device_manifest_package"></span><span id="submitting_a_multiple-locale_device_manifest_package"></span><span id="SUBMITTING_A_MULTIPLE-LOCALE_DEVICE_MANIFEST_PACKAGE"></span>提交多区域设置设备清单包


你可以使用相同的方法提交用于预览或发布的包。

**提交设备清单包**

1.  使用 [SignTool](https://go.microsoft.com/fwlink/p/?LinkId=238330) 工具对 devicemanifest-ms 程序包进行签名。

2.  从硬件开发人员中心或 Windows 开发人员中心，使用 Microsoft 帐户登录到“仪表板”。

3.  在“设备元数据”下，单击“创建体验”（如果你希望提交新体验），或单击“管理体验”（如果你希望修改现有体验）。

4.  浏览并选择你的新 devicemanifest-ms 程序包，然后单击“提交”。

## <a name="span-idcreatingadevicemanifestsubmissionpackagespanspan-idcreatingadevicemanifestsubmissionpackagespanspan-idcreatingadevicemanifestsubmissionpackagespancreating-a-device-manifest-submission-package"></a><span id="Creating_a_Device_Manifest_Submission_Package"></span><span id="creating_a_device_manifest_submission_package"></span><span id="CREATING_A_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>创建设备清单提交包


设备清单提交程序包是必须将所有多区域设置设备元数据提交到硬件开发人员中心仪表板的程序包格式。

设备清单提交程序包包含声明区域设置支持的文件。 设备清单包还包含设备元数据包。

设备清单提交程序包可以采用与设备元数据包相同的方式上载到硬件开发人员中心仪表板。 使用相同的用户界面和上传框，输入要上传的 \*.devicemanifest-ms 文件的名称。

仪表板的用户界面上批量上载以外的所有文件上载框都将接受设备清单提交包。

### <a name="span-iddevicemanifestsubmissionpackagecontentsspanspan-iddevicemanifestsubmissionpackagecontentsspanspan-iddevicemanifestsubmissionpackagecontentsspandevice-manifest-submission-package-contents"></a><span id="Device_Manifest_Submission_Package_Contents"></span><span id="device_manifest_submission_package_contents"></span><span id="DEVICE_MANIFEST_SUBMISSION_PACKAGE_CONTENTS"></span>设备清单提交包内容

每个设备清单提交包都包含以下组成部分：

-   设备元数据包

    此包包含用于在 Windows 中显示设备图标、设置操作及使用设备体验功能的信息和图片。

    设备元数据包始终必需。

-   LocaleInfo XML 文档

    此文档包含有关包含在附带设备元数据包中的区域设置的数据。 硬件开发人员中心使用此数据来正确验证一个或多个区域设置的设备元数据包。

    LocaleInfo XML 文档始终是必需的，即使设备元数据包仅包含单个区域设置。

### <a name="span-idstructureofadevicemanifestsubmissionpackagespanspan-idstructureofadevicemanifestsubmissionpackagespanspan-idstructureofadevicemanifestsubmissionpackagespanstructure-of-a-device-manifest-submission-package"></a><span id="Structure_of_a_Device_Manifest_Submission_Package"></span><span id="structure_of_a_device_manifest_submission_package"></span><span id="STRUCTURE_OF_A_DEVICE_MANIFEST_SUBMISSION_PACKAGE"></span>设备清单提交包的结构

设备清单包的结构取决于包含的设备元数据用于电脑、用于移动宽带还是包含对多个区域设置的支持。

如果设备元数据不属于这三个类别中的任何一个，则不需要设备清单包。 但是，设备清单包仍然可用于指示设备元数据包是用于单个区域设置的。

### <a name="span-idstructureofmulti-localedevicemanifestsubmissionpackagesspanspan-idstructureofmulti-localedevicemanifestsubmissionpackagesspanspan-idstructureofmulti-localedevicemanifestsubmissionpackagesspanstructure-of-multi-locale-device-manifest-submission-packages"></a><span id="Structure_of_Multi-locale_Device_Manifest_Submission_Packages"></span><span id="structure_of_multi-locale_device_manifest_submission_packages"></span><span id="STRUCTURE_OF_MULTI-LOCALE_DEVICE_MANIFEST_SUBMISSION_PACKAGES"></span>多区域设置设备清单提交包的结构

即使你的设备元数据包包含用于支持多个区域设置的信息，仍然必须在设备清单包中提交它。

设备清单提交包的组成部分存储在压缩的 Cab 文件中。 该文件名必须具有后缀 .devicemanifest-ms。

每个设备清单提交包都必须具有以下结构：

``` syntax
GUID1.devicemanifest-ms
\GUID1.devicemetadata-ms
\LocaleInfo.xml
```

“GUID1”必须是一个 GUID。

下面是有关创建 LocaleInfo.xml 的说明。

若要了解如何开发设备元数据包 \*.devicemetadata-ms，请参阅 [Windows 8 的设备元数据包架构参考](https://go.microsoft.com/fwlink/p/?LinkId=226753)。

你可以使用 Cabarc 工具创建这些 CAB 程序包。 有关此工具的详细信息，请参阅 [Cabarc 概述](https://go.microsoft.com/fwlink/p/?LinkId=248843)。

使用 Cabarc 工具创建 \*.devicemanifest-ms 文件时，必须创建一个本地目录，其中设备元数据包 (\*.devicemetadata-ms) 和 LocaleInfo XML 文档位于该目录的根目录中。

**备注**

-   .devicemanifest-ms 和 .devicemetadata-ms 文件名必须指定不带花括号 ({}) 分隔符的 GUID。

-   每个设备清单提交和设备元数据包的 GUID 都必须唯一。 当你创建新的或修改的程序包时，必须创建新 GUID。

-   有关如何创建 cabinet 文件的详细信息，请参阅 [Microsoft Cabinet 软件开发工具包](https://go.microsoft.com/fwlink/p/?LinkId=248844)。

**示例**

下面是如何使用 Cabarc 工具创建 .devicemanifest-ms 文件的示例。 在此示例中，设备清单文件的组成部分位于名为 DeviceManifestPackages 的本地目录中：

``` syntax
.\DeviceManifestPackages\
.\DeviceManifestPackages\LocaleInfo.xml
.\DeviceManifestPackages\GUID.devicemetadata-ms
```

GUID.devicemanifest-ms 文件在名为 ManifestFiles 的本地目录中创建：

``` syntax
Cabarc.exe -r -p -P  .\DeviceManifestPackages\ 
N .\ManifestFiles\ GUID.devicemanifest-ms 
.\DeviceManifestPackages\LocaleInfo.xml
.\DeviceManifestPackages\GUID.devicemetadata-ms
```

## <a name="span-idcreatinglocaleinfoxmlspanspan-idcreatinglocaleinfoxmlspancreating-localeinfoxml"></a><span id="creating_localeinfo.xml"></span><span id="CREATING_LOCALEINFO.XML"></span>创建 LocaleInfo.xml


有关创建用于提交的 Localeinfo.xml 文件的信息，请参阅[创建 LocaleInfo.xml 提交文件](https://msdn.microsoft.com/library/windows/hardware/hh801885.aspx)。

 

 





