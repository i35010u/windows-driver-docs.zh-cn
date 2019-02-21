---
title: UWP 设备应用程序的第 6 步提交设备元数据
description: 本主题介绍如何将提交到 Windows 开发人员中心硬件仪表板 UWP 设备应用的设备元数据。
ms.assetid: 5A4A371E-42A2-43C8-A496-CC3C38C17182
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16e75953f87c5fb48ee01edb45ff87bbd867eca9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522815"
---
# <a name="step-6-submit-device-metadata-for-your-uwp-device-app"></a>步骤 6：提交设备元数据为 UWP 设备应用


![设备应用工作流，步骤 6](images/6-device-app-workflow.png)

本主题介绍如何将提交到 Windows 开发人员中心硬件仪表板 UWP 设备应用的设备元数据。

UWP 设备应用程序是一种特殊的设备制造商创建作为其内部或外围设备的配套的 UWP 应用。 使用设备元数据，设备应用程序可以运行特权的操作，并在插入设备时，自动安装。 有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**请注意**  本主题是分步系列的一部分。 请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)引入。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>在开始之前


有两种方法来提交您对硬件仪表板的设备元数据包：

-   您可以提交.devicemanifest ms 文件单独向硬件仪表板。
-   可以打包多个.devicemanifest ms 文件并将其提交到大容量提交包为硬件仪表板。 可以使用创建大容量提交包**设备元数据创建向导**。

这两种方式需要文件进行签名，然后将它们提交到硬件仪表板。 您可以执行此操作通过使用**数字签名向导**。 若要打开**数字签名向导**从**设备元数据创建向导**，单击**工具**，然后单击**签名向导**.

## <a name="span-idcreatingabulksubmissionpackagespanspan-idcreatingabulksubmissionpackagespanspan-idcreatingabulksubmissionpackagespancreating-a-bulk-submission-package"></a><span id="Creating_a_bulk_submission_package"></span><span id="creating_a_bulk_submission_package"></span><span id="CREATING_A_BULK_SUBMISSION_PACKAGE"></span>创建大容量提交包


可以使用**大容量包向导**以创建可以立即提交到硬件仪表板的多个 devicemanifest ms 文件的大容量提交包。 您使用**设备元数据创建向导**以打开**大容量包向导**。

**若要创建大容量提交包**

1.  在中**设备元数据创建向导**，单击**工具**，然后单击**创建大容量包**。
2.  在中**大容量包向导**，为每个.devicemanifest ms 文件，执行以下操作：
    -   单击**添加元数据包**。
    -   浏览到.devicemanifest ms 文件，然后依次**确定**。

3.  选择**预览版**应在预览模式下提交每个.devicemanifest ms 文件旁边的复选框。
4.  已添加的所有.devicemanifest ms 文件后，单击**下一步**。
5.  上**指定的设备体验信息**页上，添加以下：
    -   **遇到名称**应该是在由你的公司已提交的其他体验名称是唯一的名称。
    -   **限定**指示如果硬件提交与此提交相关联。 如果相关联的硬件提交，请选择**此设备具有相关联的硬件或未分类的提交**。
    -   **徽标提交 Id**应包括硬件仪表板提交 Id。
    -   **更新体验**如果之前已提交的体验，则应选择。

    **请注意**  提交设备元数据为 UWP 设备应用之前必须经过认证设备。

     

6.  上**准备大容量包提交**页上，单击**启动签名向导**以启动**数字签名向导**，用于进行数字签名在大容量提交包。

提交设备元数据包到硬件仪表板的详细信息，请参阅[设备元数据](https://msdn.microsoft.com/library/windows/hardware/br230800.aspx)。

 

 





