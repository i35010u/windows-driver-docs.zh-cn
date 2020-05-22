---
title: 在 Visual Studio 中创建服务元数据提交包
description: 在 Visual Studio 中创建服务元数据提交包
ms.assetid: 93C2F66B-EAD3-4C7B-A761-E0AF861101D0
keywords:
- 在 Visual Studio 中创建服务元数据提交包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cef866f572eeeeb80afab105a978bf36cadeb669
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769531"
---
# <a name="creating-a-service-metadata-submission-package-in-visual-studio"></a>在 Visual Studio 中创建服务元数据提交包


使用 Microsoft Visual Studio 中的提交工具创建提交包。

### <a name="span-idto_create_a_submission_packagespanspan-idto_create_a_submission_packagespanspan-idto_create_a_submission_packagespanto-create-a-submission-package"></a><span id="To_create_a_submission_package"></span><span id="to_create_a_submission_package"></span><span id="TO_CREATE_A_SUBMISSION_PACKAGE"></span>创建提交包

1.  单击 "**驱动程序**" 菜单，选择 "**设备元数据**"，然后选择 "**提交**"。
2.  单击 "**添加元数据包**"，查找并选择元数据包，并单击 "**打开**"。
3.  确认**包名称**和**型号名称**，然后选择 "**预览**" （如果要预览包）。

    **注意**   "**模型名称**" 字段是服务**提供商**名称，它是作为服务元数据包的一部分指定的。

     

4.  单击 **下一步**。
5.  查看**模型名称**、**硬件 ID**和**体验 ID**。
6.  在 "**体验名称**" 旁边，键入体验的名称。
    **注意**   所有包提交都需要执行此步骤。

     

7.  在 "**限定**" 旁边，选择 "**此设备具有关联的徽标或**从列表中未分类的提交"。
8.  如果之前已提交了包，请选择 "**更新体验**"。
9.  单击 **下一步**。
10. 重新输入硬件 ID 信息（例如，IMSI 或 ICCID），确认移动宽带提供商的信息。 Windows 开发人员中心中的 "硬件" 面板使用纯文本硬件 ID 信息来验证元数据包中指定的哈希硬件 Id。
11. 如果尚未对包进行签名，请按照以下步骤对其进行签名：

    1.  找到证书文件，然后双击该文件进行安装。
    2.  请确保在用户存储中安装证书文件，而不是计算机存储。
    3.  单击 "**启动签名向导**"。
    4.  单击 "**选择存储**"。
    5.  从对话框中选择证书。
        **注意**   签名向导中的文件名是完成提交元数据向导后收到的内容。 因此，除非有特定原因，否则请不要更改文件名或路径。

         

    6.  完成签名过程。

12. 准备好提交包时，单击 "**启动 Windows 开发人员中心-硬件仪表板**"。

有关如何提交包的详细信息，请参阅[提交设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-device-metadata-package--dashboard-help-)。

有关设备清单文件的详细信息，请参阅[提交移动宽带设备清单包](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-mobile-broadband-device-manifest-package)。

有关 bulkmetadata 文件的详细信息，请参阅[提交批量元数据包](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-bulk-metadata-package)。

 

 





