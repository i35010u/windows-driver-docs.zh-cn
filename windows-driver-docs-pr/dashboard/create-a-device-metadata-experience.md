---
title: 创建设备元数据体验
description: 创建设备元数据体验
ms.assetid: 964ad06e-0f29-441d-b184-61f80a614914
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47ae6c7fdeeb735b1a2c827804cd147527206d36
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364465"
---
# <a name="create-a-device-metadata-experience"></a>创建设备元数据体验


在你创建设备元数据文件（.devicemetadata-ms 或 .devicemanifest-ms，这些文件提供让你的设备更易于识别的图像和其他功能）后，你必须将它们作为体验。

devicemanifest-ms 文件是一个 .cab 文件，其中包含 devicemetadata-ms 文件及多区域设置包、计算机包和移动宽带帐户体验包等其他信息。 对于所有 devicemanifest-ms 包，其他信息必须包含在 LocaleInfo.xml 文件中。 有关详细信息，请参阅 PcMetadataSubmission.xml MobileBroadbandMetadataSubmission.xml 创建页。

## <a name="span-idcreating_a_device_metadata_experience_packagespanspan-idcreating_a_device_metadata_experience_packagespanspan-idcreating_a_device_metadata_experience_packagespancreating-a-device-metadata-experience-package"></a><span id="Creating_a_device_metadata_experience_package"></span><span id="creating_a_device_metadata_experience_package"></span><span id="CREATING_A_DEVICE_METADATA_EXPERIENCE_PACKAGE"></span>创建设备元数据体验包


在你可以提交文件进行徽标认证之前，你必须将这些文件打包到一个体验中。 此体验也是将具有完全相同的硬件 ID 和型号 ID 集但具有不同区域设置的设备的设备元数据包编组到一起的一种方法。

**创建设备元数据体验包**

1. 使用与此服务关联的 Microsoft 帐户从合作伙伴中心登录到仪表板。

2. 在窗口左侧，单击“设备元数据”  ，然后单击“创建体验”  。

3. 在“创建体验”  页上，输入以下信息：

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>字段</th>
   <th>说明</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td><p>体验名称</p></td>
   <td><p>为体验创建一个不同于你的公司已产生的所有其他体验名称的名称。</p></td>
   </tr>
   <tr class="even">
   <td><p>包友好名称</p></td>
   <td><p>如有必要，创建一个更易于使用和记住的名称。</p></td>
   </tr>
   <tr class="odd">
   <td><p>文件</p></td>
   <td><p>浏览以查找并上载你要包含在你的体验中的多达 50 个文件。</p></td>
   </tr>
   <tr class="even">
   <td><p>预览包</p></td>
   <td><p>如果你要将你选择的所有程序包提交为预览包，请选择此项。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/" data-raw-source="[Creating a Preview Package](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)">创建预览包</a>。</p></td>
   </tr>
   <tr class="odd">
   <td><p>绑定到徽标提交</p></td>
   <td><p>如果你要提交的设备仅使用内置驱动程序且没有徽标认证，请选择第一个选项。 如果你的设备有关联的徽标提交，你的设备是电脑、打印机、传真机或扫描仪，或者如果你的元数据用于一系列移动宽带帐户标识符，请选择第二个选项。</p></td>
   </tr>
   <tr class="even">
   <td><p>绑定到徽标提交：选择提交</p></td>
   <td><p>如果你选择第二个选项，并且你为计算机、移动宽带帐户体验或者 IDDA 列表上的打印机或传真机提交元数据，则不必绑定任何徽标提交。</p>
   <p>如果你选择第二个选项，并且你为任何其他类型的设备提交元数据，则必须选择并绑定适用于你的设备的徽标提交。</p></td>
   </tr>
   </tbody>
   </table>

     

4. 单击“提交”  。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[管理设备元数据体验](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

[提交批量元数据包](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

[提交设备元数据体验时的错误和解决方案](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

[设备元数据业务规则](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

 

 






