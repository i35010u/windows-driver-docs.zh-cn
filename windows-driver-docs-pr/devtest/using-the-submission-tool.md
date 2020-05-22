---
title: 在 Visual Studio 中创建设备元数据提交包
description: 在 Visual Studio 中创建设备元数据提交包
ms.assetid: 17CF8185-C9EE-4B25-BEE7-A1FFB8C92EE0
keywords:
- 在 Visual Studio 中创建设备元数据提交包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9620ebccd59ad84eb556771421cfd082ab8bb82
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769691"
---
# <a name="creating-a-device-metadata-submission-package-in-visual-studio"></a>在 Visual Studio 中创建设备元数据提交包


若要创建设备元数据提交包，请使用 Microsoft Visual Studio 中的提交工具。

1.  在 Visual Studio 中，单击 "**驱动程序**" 菜单，选择 "**设备元数据**"，然后选择 "**提交**"。
2.  单击 "**添加元数据包**"，选择包，然后单击 "**打开**"。
3.  确认**包名称**和**型号名称**，选择 "**预览**" （如果要预览包），然后单击 "**下一步**"。
4.  查看**模型名称**、**硬件 ID**和**体验 ID**。
5.  在 "**体验名称**" 旁边，键入体验的名称。
    **注意**   所有包提交都需要执行此步骤。

     

6.  在 "**限定**" 旁边，从列表中选择下列选项之一：
    -   **此设备有关联的徽标或未分类的提交**
        -   输入**徽标提交 id**。
    -   **此设备仅使用收件箱驱动程序，并且没有关联的徽标提交**

7.  如果之前已提交了包，请选择 "**更新体验**"。
8.  单击 **下一步**。
9.  如果尚未对包进行签名，请在签名向导中完成以下步骤对其进行签名：

    1.  找到证书文件，然后双击该文件进行安装。
    2.  请确保将证书文件安装在用户存储中，而不是安装在计算机存储区中。
    3.  单击 "**启动签名向导**"。
    4.  单击 "**选择存储**"。
    5.  从对话框中选择证书。
        **注意**   签名向导中的文件名是完成提交元数据向导后收到的内容。 因此，除非有特定原因，否则请不要更改文件名或路径。

         

    6.  完成签名过程。

10. 准备好提交包时，单击 "**启动 Windows 开发人员中心-硬件仪表板**"。

有关如何提交包的详细信息，请参阅[提交设备元数据包](hhttps://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-device-metadata-package--dashboard-help-)。

有关 bulkmetadata 文件的详细信息，请参阅[提交批量元数据包](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-bulk-metadata-package)。

 

 





