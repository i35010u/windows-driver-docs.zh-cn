---
title: 在 Visual Studio 中创建服务元数据提交包
description: 在 Visual Studio 中创建服务元数据提交包
ms.assetid: 93C2F66B-EAD3-4C7B-A761-E0AF861101D0
keywords:
- 在 Visual Studio 中创建服务元数据提交包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad5168e4e74f1fb56cdd6c4cb92dd548ff857cc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521613"
---
# <a name="creating-a-service-metadata-submission-package-in-visual-studio"></a>在 Visual Studio 中创建服务元数据提交包


使用 Microsoft Visual Studio 中提交工具创建提交包。

### <a name="span-idtocreateasubmissionpackagespanspan-idtocreateasubmissionpackagespanspan-idtocreateasubmissionpackagespanto-create-a-submission-package"></a><span id="To_create_a_submission_package"></span><span id="to_create_a_submission_package"></span><span id="TO_CREATE_A_SUBMISSION_PACKAGE"></span>若要创建提交包

1.  单击**驱动程序**菜单中，选择**设备元数据**，然后选择**提交**。
2.  单击**添加元数据包**，找到并选择元数据包，然后单击**打开**。
3.  确认**包名称**并**模型名称**，然后选择**预览**如果你想要预览包。

    **请注意**  **模型名称**字段是**服务提供商**指定为服务元数据包的一部分的名称。

     

4.  单击“下一步” 。
5.  审阅**模型名称**，**硬件 Id**，并**体验 ID**。
6.  下一步**遇到名称**，键入体验的名称。
    **请注意**  的所有包提交，则需要此步骤。

     

7.  下一步**限定**，选择**此设备具有关联的徽标或未分类的提交**从列表中。
8.  如果包已提交之前，请选择**更新体验**。
9.  单击“下一步” 。
10. 通过重新输入的硬件 ID 信息 （例如，IMSI 或 ICCID） 确认移动宽带提供商的信息。 Windows 开发人员中心硬件仪表板使用纯文本的硬件 ID 信息以验证经过哈希处理的元数据包中指定的硬件 Id。
11. 如果你尚未登录你的包，请执行以下步骤来对其进行签名：

    1.  找到证书文件，然后双击它以安装它。
    2.  请确保在用户存储和不在计算机存储中安装该证书文件。
    3.  单击**启动签名向导**。
    4.  单击**选择应用商店**。
    5.  从对话框中选择的证书。
        **请注意**  签名向导中的文件名称是你接收完成提交元数据向导后。 因此，除非有特定原因，否则不要更改文件名或路径。

         

    6.  完成签名过程。

12. 如果你已准备好提交包，单击**启动 Windows 开发人员中心-硬件仪表板**。

有关如何提交包的详细信息，请参阅[提交设备元数据包](https://go.microsoft.com/fwlink/p/?linkid=226302)。

有关 devicemanifest 文件的详细信息，请参阅[UWP 应用程序提交用于移动宽带](https://go.microsoft.com/fwlink/p/?linkid=248426)。

有关 bulkmetadata 文件的详细信息，请参阅[提交批量元数据包](https://go.microsoft.com/fwlink/p/?linkid=248427)。

 

 





