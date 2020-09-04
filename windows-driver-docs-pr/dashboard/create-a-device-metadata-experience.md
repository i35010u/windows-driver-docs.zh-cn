---
title: 创建设备元数据体验
description: 创建设备元数据体验
ms.assetid: 964ad06e-0f29-441d-b184-61f80a614914
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d7f337c17039a4e70dfa22369b26079794c96ae
ms.sourcegitcommit: bd72676caf2bf5c9738c4081c778316919b85d30
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89450030"
---
# <a name="create-a-device-metadata-experience"></a>创建设备元数据体验

在你创建设备元数据文件（.devicemetadata-ms 或 .devicemanifest-ms，这些文件提供让你的设备更易于识别的图像和其他功能）后，你必须将它们作为体验。

devicemanifest-ms 文件是一个 .cab 文件，其中包含 devicemetadata-ms 文件及多区域设置包、计算机包和移动宽带帐户体验包等其他信息。 对于所有 devicemanifest-ms 包，其他信息必须包含在 LocaleInfo.xml 文件中。 有关详细信息，请参阅 PcMetadataSubmission.xml MobileBroadbandMetadataSubmission.xml 创建页。

## <a name="creating-a-device-metadata-experience-package"></a>创建设备元数据体验包

在你可以提交文件进行徽标认证之前，你必须将这些文件打包到一个体验中。 此体验也是将具有完全相同的硬件 ID 和型号 ID 集但具有不同区域设置的设备的设备元数据包编组到一起的一种方法。

### <a name="to-create-a-device-metadata-experience-package"></a>创建设备元数据体验包

1. 使用与此服务关联的 Microsoft 帐户从合作伙伴中心登录到仪表板。

2. 在窗口左侧，单击“设备元数据”  ，然后单击“创建体验”  。

3. 在“创建体验”  页上，输入以下信息：


|字段|说明|
|----|----|
|体验名称|为体验创建一个不同于你的公司已产生的所有其他体验名称的名称。|
|包友好名称|如有必要，创建一个更易于使用和记住的名称。|
|文件|浏览以查找并上载你要包含在你的体验中的多达 50 个文件。|
|预览包|如果你要将你选择的所有程序包提交为预览包，请选择此项。 有关详细信息，请参阅[创建预览包](creating-a-preview-package.md)。|
|绑定到徽标提交|如果你要提交的设备仅使用内置驱动程序且没有徽标认证，请选择第一个选项。 如果你的设备有关联的徽标提交，你的设备是电脑、打印机、传真机或扫描仪，或者如果你的元数据用于一系列移动宽带帐户标识符，请选择第二个选项。|
|绑定到徽标提交：选择提交|如果你选择第二个选项，并且你为计算机、移动宽带帐户体验或者 IDDA 列表上的打印机或传真机提交元数据，则不必绑定任何徽标提交。</br>如果你选择第二个选项，并且你为任何其他类型的设备提交元数据，则必须选择并绑定适用于你的设备的徽标提交。|

4. 单击“提交”  。

## <a name="related-topics"></a>相关主题

[管理设备元数据体验](manage-device-metadata-experiences.md)

[提交批量元数据包](submit-a-bulk-metadata-package.md)

[提交设备元数据体验时的错误和解决方案](errors-and-solutions-when-submitting-device-metadata-experiences.md)

[设备元数据业务规则](device-metadata-business-rules.md)
