---
title: 步骤6提交 UWP 设备应用的设备元数据
description: 本主题介绍如何向 Windows 开发人员中心硬件仪表板提交 UWP 设备应用的设备元数据。
ms.assetid: 5A4A371E-42A2-43C8-A496-CC3C38C17182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f7f0ba76659c8ed5bc9bd2c9956576d9568708
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097401"
---
# <a name="step-6-submit-device-metadata-for-your-uwp-device-app"></a>步骤6：提交 UWP 设备应用的设备元数据


![设备应用工作流，步骤6](images/6-device-app-workflow.png)

本主题介绍如何向 Windows 开发人员中心硬件仪表板提交 UWP 设备应用的设备元数据。

UWP 设备应用是一种特殊类型的 UWP 应用，设备制造商可以创建它来充当其内部或外围设备。 通过使用设备元数据，设备应用可以运行特权操作并在设备接通电源时自动安装。 有关 UWP 设备应用的详细信息，请参阅 " [满足 uwp 设备应用](meet-uwp-device-apps.md)"。

**注意**   本主题是分步序列的一部分。 有关简介，请参阅 [构建 UWP 设备应用循序渐进](build-a-uwp-device-app-step-by-step.md) 。

 

## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前


可以通过两种方式将设备元数据包提交到硬件仪表板：

-   可以将 devicemanifest-ms 文件逐个提交到硬件仪表板。
-   可以将多个 devicemanifest 文件打包在一起，并将其作为大容量提交包提交给硬件仪表板。 您可以使用 **设备元数据创作向导**来创建大容量提交包。

这两种方法都要求在将文件提交到硬件仪表板之前对文件进行签名。 可以使用 **数字签名向导**来执行此操作。 若要从**设备元数据创作向导**打开**数字签名向导**，请单击 "**工具**"，然后单击 "**签名向导**"。

## <a name="span-idcreating_a_bulk_submission_packagespanspan-idcreating_a_bulk_submission_packagespanspan-idcreating_a_bulk_submission_packagespancreating-a-bulk-submission-package"></a><span id="Creating_a_bulk_submission_package"></span><span id="creating_a_bulk_submission_package"></span><span id="CREATING_A_BULK_SUBMISSION_PACKAGE"></span>创建批量提交包


你可以使用 **批量包向导** 来创建大容量提交包，以便一次将多个 devicemanifest-ms 文件提交到硬件仪表板。 您可以使用 **设备元数据创作向导** 打开 **大容量包向导**。

**创建批量提交包**

1.  在 **设备元数据创作向导**中，单击 " **工具**"，然后单击 " **创建大容量包**"。
2.  在 **批量包向导**中，为每个 devicemanifest 文件执行以下操作：
    -   单击 " **添加元数据包**"。
    -   浏览到 "devicemanifest" 文件，然后单击 **"确定"**。

3.  选中应在预览模式下提交的每个 devicemanifest 文件旁边的 " **预览** " 复选框。
4.  添加所有 devicemanifest-ms 文件后，单击 " **下一步**"。
5.  在 " **指定设备体验信息** " 页上，添加以下内容：
    -   **体验名称** 应为在公司提交的其他体验名称中唯一的名称。
    -   "**限定**" 指示是否将硬件提交与此提交相关联。 如果有关联的硬件提交，请选择 " **此设备有关联的硬件或未分类的提交**"。
    -   **徽标提交 id** 应该包含硬件仪表板提交 id。
    -   如果已提交经验，则应选择 "**更新体验**"。

    **注意**   必须先认证设备，然后才能提交 UWP 设备应用的设备元数据。

     

6.  在 " **准备批量包以提交** " 页上，单击 " **启动签名向导** " 以启动 " **数字签名向导**"，该向导用于对大容量提交包进行数字签名。

有关将设备元数据包提交到硬件仪表板的详细信息，请参阅 [设备元数据](../dashboard/index.yml)。

 

