---
title: 第 5 步提交 Microsoft Store 设备应用程序
description: 本主题介绍如何将 UWP 设备应用提交到 Microsoft Store 仪表板。
ms.assetid: B25F9953-6EFD-4A08-AFD6-B334C46E910F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92891a52939342af36043ee4601db0e072524101
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565569"
---
# <a name="step-5-submit-the-microsoft-store-device-app"></a>步骤 5：将 Microsoft Store 设备应用程序提交


![设备应用工作流，第 5 步](images/5-device-app-workflow.png)

本主题介绍如何将 UWP 设备应用提交到 Microsoft Store 仪表板。 在提交之前您的应用程序，请查看中的提交序列部分[构建 UWP 设备应用](the-workflow.md)。 本主题是分步系列的一部分。 请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)引入。

**请注意**  如果您的应用程序指定为特权的应用程序并不将其配置为自动安装，可以将之前提交到特权应用程序提交到 Windows 开发人员中心硬件仪表板在设备元数据Microsoft Store。 在这种情况下，此步骤 5 可以发生[第 6 步](step-6--submit-device-metadata.md)。

 

UWP 设备应用程序是一种特殊的设备制造商创建作为其内部或外围设备的配套的 UWP 应用。 通过使用设备元数据，设备应用程序可以运行特权的操作，如设备更新。 有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前的准备工作


本主题假定你已完成开发您的应用程序和设备元数据已准备就绪。

## <a name="span-idstartappsubmissionspanspan-idstartappsubmissionspanspan-idstartappsubmissionspanstart-app-submission"></a><span id="Start_app_submission"></span><span id="start_app_submission"></span><span id="START_APP_SUBMISSION"></span>启动应用程序提交


转到[Microsoft Store 仪表板](https://go.microsoft.com/fwlink/p/?LinkId=273050)然后单击**提交新应用程序**。

## <a name="span-idaddinstructionsfortestersspanspan-idaddinstructionsfortestersspanspan-idaddinstructionsfortestersspanadd-instructions-for-testers"></a><span id="Add_instructions_for_testers"></span><span id="add_instructions_for_testers"></span><span id="ADD_INSTRUCTIONS_FOR_TESTERS"></span>添加测试人员的说明


在中**面向测试人员说明**，请确保您输入的文本"这是 UWP 设备应用程序"。 这指示应用程序提交测试人员，您的应用程序是 UWP 设备应用。

## <a name="span-idreviewsubmissiondetailsspanspan-idreviewsubmissiondetailsspanspan-idreviewsubmissiondetailsspanreview-submission-details"></a><span id="Review_submission_details"></span><span id="review_submission_details"></span><span id="REVIEW_SUBMISSION_DETAILS"></span>查看提交详细信息


在提交您的应用程序之前，请检查以下各项：

-   应用的说明应清楚地说明应用所需的硬件。

-   您必须在 Microsoft Store 以将应用程序识别为 UWP 设备应用的应用程序包中包括 StoreManifest.xml 文件。

-   启动应用时，如果应用需要先连接设备，然后应用将正常工作，它必须明确声明类似于"请连接你&lt;*特定于标记的设备名称*&gt;"。

-   **包名称**应为一个创建的应用程序中时指定相同[第 1 步](step-1--create-a-uwp-device-app.md)。 请注意，是否在一年内不提交应用，包名称时到期。

-   该应用程序必须完全符合所有[Microsoft Store 认证要求](https://go.microsoft.com/fwlink/p/?LinkId=273052)。

-   应用必须适用于各年龄阶段。

-   应用程序必须标记为可用。

## <a name="span-idconfirmsellingdetailsspanspan-idconfirmsellingdetailsspanspan-idconfirmsellingdetailsspanconfirm-selling-details"></a><span id="Confirm_selling_details"></span><span id="confirm_selling_details"></span><span id="CONFIRM_SELLING_DETAILS"></span>确认销售详细信息


在应用程序提交过程中检查**销售详细信息**项存储区提交清单，并确保你看到此：

**您的应用程序必须是自由，因为它是 UWP 设备应用。**

**您的应用程序将免费销售后它通过了认证，schedued 版。**

应用程序提交 UI 旨在寻找 StoreManifest.xml，以检查应用程序是否与设备关联的 UWP 设备应用程序的唯一方式。 一旦它使决定，它将显式重写设置的任何销售详细信息中以确保应用程序设置为使用任何试用版免费和 (和禁用的控件，如果您尝试更改这些值在**销售详细信息**页）。 然后反映在清单页上。

如果没有看到**您的应用程序必须是自由，因为它是 UWP 设备应用**中**销售详细信息**页上，检查是否已正确应用项目，而不是在根文件夹中包含 StoreManifest.xml解决方案的根文件夹。

## <a name="span-idsubmissionresultsspanspan-idsubmissionresultsspanspan-idsubmissionresultsspansubmission-results"></a><span id="Submission_results"></span><span id="submission_results"></span><span id="SUBMISSION_RESULTS"></span>提交结果


一旦 Microsoft Store 收到您的应用程序，它将执行一套通用的所有 UWP 应用的自动测试。 它还会执行一系列特定于应用程序的测试。

如果您的应用程序通过 Microsoft Store 应用测试后，它将添加到应用程序目录在大约 1-4 天。 在目录中后，也可以从 Microsoft Store 以及。 如果提交失败，则会通知您有关原因。

## <a name="span-idvalidationspanspan-idvalidationspanspan-idvalidationspanvalidation"></a><span id="Validation"></span><span id="validation"></span><span id="VALIDATION"></span>验证


Microsoft Store 仪表板提交到 Microsoft Store 后验证 Microsoft Store 设备应用程序包。 设备元数据提交到并由 Windows 开发人员中心硬件仪表板进行验证。 应用将在 Microsoft Store 中，由于验证过程会检查指定的元数据中的应用位于存储区后，您应提交元数据。 硬件仪表板徽标提交的一部分单独验证驱动程序。

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤 6：提交设备元数据](step-6--submit-device-metadata.md)

 

 





