---
title: 在 Visual Studio 中创建设备元数据提交包
description: 在 Visual Studio 中创建设备元数据提交包
ms.assetid: 17CF8185-C9EE-4B25-BEE7-A1FFB8C92EE0
keywords:
- 在 Visual Studio 中创建设备元数据提交包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67d801b660fcf3cfbc1bb48e351ce06de2c8abdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544326"
---
# <a name="creating-a-device-metadata-submission-package-in-visual-studio"></a>在 Visual Studio 中创建设备元数据提交包


若要创建设备元数据提交包，使用 Microsoft Visual Studio 中的提交工具。

1.  在 Visual Studio 中，单击**驱动程序**菜单中，选择**设备元数据**，然后选择**提交**。
2.  单击**添加元数据包**，选择的包，然后单击**打开**。
3.  确认**包名称**并**模型名称**，选择**预览**如果想以预览包，然后单击**下一步**。
4.  审阅**模型名称**，**硬件 Id**，并**体验 ID**。
5.  下一步**遇到名称**，键入体验的名称。
    **请注意**  的所有包提交，则需要此步骤。

     

6.  下一步**限定**，从列表中的以下一个选项的选择：
    -   **此设备具有关联的徽标或未分类的提交**
        -   输入**徽标提交 Id**。
    -   **此设备使用收件箱驱动程序，并且有任何关联的徽标提交**

7.  如果包已提交之前，请选择**更新体验**。
8.  单击“下一步” 。
9.  如果你尚未登录你的包，请完成签名向导对其进行签名中的以下步骤：

    1.  找到证书文件，然后双击它以安装它。
    2.  请确保在用户存储中并不在计算机存储中安装该证书文件。
    3.  单击**启动签名向导**。
    4.  单击**选择应用商店**。
    5.  从对话框中选择的证书。
        **请注意**  签名向导中的文件名称是你接收完成提交元数据向导后。 因此，除非有特定原因，否则不要更改文件名或路径。

         

    6.  完成签名过程。

10. 如果你已准备好提交包，单击**启动 Windows 开发人员中心-硬件仪表板**。

有关如何提交包的详细信息，请参阅[提交设备元数据包](https://go.microsoft.com/fwlink/p/?linkid=226302)。

有关 bulkmetadata 文件的详细信息，请参阅[提交批量元数据包](https://go.microsoft.com/fwlink/p/?linkid=248427)。

 

 





