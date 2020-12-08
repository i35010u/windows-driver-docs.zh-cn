---
title: 步骤5提交 Microsoft Store 设备应用
description: 本主题介绍如何将 UWP 设备应用提交到 Microsoft Store 仪表板。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28c20d0f9c15fe48f782b156d3f774d43fb31ce3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802665"
---
# <a name="step-5-submit-the-microsoft-store-device-app"></a>步骤5：提交 Microsoft Store 设备应用


![设备应用工作流，步骤5](images/5-device-app-workflow.png)

本主题介绍如何将 UWP 设备应用提交到 Microsoft Store 仪表板。 提交应用之前，请查看 [生成 UWP 设备应用](the-workflow.md)中的提交序列部分。 本主题是分步序列的一部分。 有关简介，请参阅 [构建 UWP 设备应用循序渐进](build-a-uwp-device-app-step-by-step.md) 。

**注意**  如果你的应用被指定为特权应用并且未配置为自动安装，你可以将你的设备元数据提交到 Windows 开发人员中心硬件仪表板，然后将特权应用提交到 Microsoft Store。 在这种情况下，可以在 [步骤 6](step-6--submit-device-metadata.md)后执行此步骤5。

 

UWP 设备应用是一种特殊类型的 UWP 应用，设备制造商可以创建它来充当其内部或外围设备。 通过使用设备元数据，设备应用可以运行特权操作，如设备更新。 有关 UWP 设备应用的详细信息，请参阅 " [满足 uwp 设备应用](meet-uwp-device-apps.md)"。

## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前


本主题假定您已完成应用程序的开发，设备元数据已准备就绪。

## <a name="span-idstart_app_submissionspanspan-idstart_app_submissionspanspan-idstart_app_submissionspanstart-app-submission"></a><span id="Start_app_submission"></span><span id="start_app_submission"></span><span id="START_APP_SUBMISSION"></span>开始应用提交


中转到 [Microsoft Store 仪表板](https://go.microsoft.com/fwlink/p/?LinkId=273050) ，并单击 " **提交新应用**"。

## <a name="span-idadd_instructions_for_testersspanspan-idadd_instructions_for_testersspanspan-idadd_instructions_for_testersspanadd-instructions-for-testers"></a><span id="Add_instructions_for_testers"></span><span id="add_instructions_for_testers"></span><span id="ADD_INSTRUCTIONS_FOR_TESTERS"></span>为测试人员添加说明


在 **测试人员的说明** 中，请确保输入文本 "这是 UWP 设备应用"。 这向应用提交测试人员表明你的应用是 UWP 设备应用。

## <a name="span-idreview_submission_detailsspanspan-idreview_submission_detailsspanspan-idreview_submission_detailsspanreview-submission-details"></a><span id="Review_submission_details"></span><span id="review_submission_details"></span><span id="REVIEW_SUBMISSION_DETAILS"></span>查看提交详细信息


提交应用之前，请先检查以下内容：

-   应用说明应清楚地说明应用所需的硬件。

-   必须将 StoreManifest.xml 文件包含在应用包中，Microsoft Store 才能将应用识别为 UWP 设备应用。

-   当应用程序启动时，如果应用程序要求在应用程序运行之前连接设备，则它必须明确说明 "请连接 &lt; *特定品牌的设备名称*" 之类的内容 &gt; 。

-   **包名称** 应与在 [步骤 1](step-1--create-a-uwp-device-app.md)中创建应用时指定的名称相同。 请注意，如果应用在一年内未提交，包名称将过期。

-   应用必须完全符合所有 [Microsoft Store 认证要求](/windows/uwp/publish/the-app-certification-process)。

-   应用必须适用于所有年龄段。

-   应用必须标记为可用。

## <a name="span-idconfirm_selling_detailsspanspan-idconfirm_selling_detailsspanspan-idconfirm_selling_detailsspanconfirm-selling-details"></a><span id="Confirm_selling_details"></span><span id="confirm_selling_details"></span><span id="CONFIRM_SELLING_DETAILS"></span>确认销售详细信息


在应用提交期间，查看存储提交清单中的 **销售详细信息** 项，并确保看到：

**应用必须免费，因为它是 UWP 设备应用。**

**你的应用将免费销售，并在通过认证后 schedued 发布。**

应用提交 UI 旨在查找 StoreManifest.xml 作为检查应用是否为与设备关联的 UWP 设备应用的唯一方法。 完成这一决定后，它将显式覆盖在销售详细信息中设置的任何内容，以确保应用设置为免费且不进行试用 (并禁用控件（如果尝试在 **销售详细信息** 页) 中更改这些值）。 然后，将反映在 "清单" 页上。

如果你看不到 **你的应用程序，因为它是** "销售" **详细信息** 页中的 UWP 设备应用，请检查你是否已将 StoreManifest.xml 正确地包含在应用项目的根文件夹中，而不是放在解决方案的根文件夹中。

## <a name="span-idsubmission_resultsspanspan-idsubmission_resultsspanspan-idsubmission_resultsspansubmission-results"></a><span id="Submission_results"></span><span id="submission_results"></span><span id="SUBMISSION_RESULTS"></span>提交结果


Microsoft Store 收到你的应用后，它将执行一套适用于所有 UWP 应用的自动测试。 它还将执行一系列特定于应用的测试。

如果你的应用程序通过 Microsoft Store 应用的测试，将在大约1-4 天内将其添加到应用程序目录。 一旦在目录中，也可以从 Microsoft Store 获取它。 如果提交失败，你将收到有关原因的通知。

## <a name="span-idvalidationspanspan-idvalidationspanspan-idvalidationspanvalidation"></a><span id="Validation"></span><span id="validation"></span><span id="VALIDATION"></span>检查


Microsoft Store 仪表板在将 Microsoft Store 设备应用包提交到 Microsoft Store 后对其进行验证。 设备元数据提交到 Windows 开发人员中心硬件仪表板并进行验证。 你应在应用程序在 Microsoft Store 上生存后提交元数据，因为验证过程会检查元数据中指定的应用是否在存储中。 在提交徽标时，硬件仪表板单独验证驱动程序。

## <a name="span-idnext_stepspanspan-idnext_stepspanspan-idnext_stepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤6：提交设备元数据](step-6--submit-device-metadata.md)

 

