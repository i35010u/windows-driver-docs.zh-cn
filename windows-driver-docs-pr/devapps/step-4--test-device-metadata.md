---
title: 步骤4测试 UWP 设备应用的设备元数据
description: 本主题介绍如何在将 UWP 设备应用提交到 Windows 开发人员中心仪表板之前，对其进行本地测试。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1bc5c33afa0d8cff9f449e473034ea5c24c9863
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802701"
---
# <a name="step-4-test-the-device-metadata-for-your-uwp-device-app"></a>步骤4：测试 UWP 设备应用的设备元数据


![设备应用工作流，步骤4](images/4-device-app-workflow.png)

本主题介绍如何在将 UWP 设备应用提交到 Windows 开发人员中心仪表板之前，对其进行本地测试。

UWP 设备应用是一种特殊类型的 UWP 应用，设备制造商可以创建它来充当其内部或外围设备。 通过使用设备元数据，设备应用可以运行特权操作并在设备接通电源时自动安装。 有关 UWP 设备应用的详细信息，请参阅 " [满足 uwp 设备应用](meet-uwp-device-apps.md)"。

**注意**  本主题是分步序列的一部分。 有关简介，请参阅 [构建 UWP 设备应用循序渐进](build-a-uwp-device-app-step-by-step.md) 。

 

## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前


可以将设备元数据部署到本地计算机上的本地设备元数据存储，以便可以测试设备是否正常工作。 一旦部署了设备元数据，它的行为方式应与提交到 Windows 开发人员中心仪表板的方式相同。 例如，如果在设备元数据中为设备启用了自动播放，则在插入设备时，自动播放处理程序应正常工作。 如果更改了模型或发布者名称，则可以确保这些更改也会显示。

在测试你的设备元数据之前，应在你将在其中部署设备元数据的计算机上安装 Microsoft Store 应用。

## <a name="span-iddeploy_your_device_metadata_locallyspanspan-iddeploy_your_device_metadata_locallyspanspan-iddeploy_your_device_metadata_locallyspandeploy-your-device-metadata-locally"></a><span id="Deploy_your_device_metadata_locally"></span><span id="deploy_your_device_metadata_locally"></span><span id="DEPLOY_YOUR_DEVICE_METADATA_LOCALLY"></span>在本地部署设备元数据


在测试你的设备元数据之前，你必须将其部署到本地设备元数据存储。 为此，您可以在创建设备元数据时选中 "将 **设备元数据包复制到本地计算机上的元数据存储区** " 复选框，或者在创建设备元数据后使用 **设备元数据创作向导** 来执行此操作。

**使用设备元数据创作向导部署设备元数据**

1.  从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin x86 中打开 **设备元数据创作向导** \\ \\ \\ \\ 。
2.  在 " **工具** " 菜单上，单击 " **部署元包**"。
3.  浏览到 "devicemetadata" 文件，然后单击 "打开" **。**
4.  如果此时出现 “用户帐户控制” 对话框，请单击 **“是”** 。
5.  部署设备元数据后，你将看到一条消息，指出已 **成功将设备元数据包复制到此计算机上的本地元数据存储**。 你的设备元数据已准备好进行测试。

## <a name="span-idvalidate_your_device_metadataspanspan-idvalidate_your_device_metadataspanspan-idvalidate_your_device_metadataspanvalidate-your-device-metadata"></a><span id="Validate_your_device_metadata"></span><span id="validate_your_device_metadata"></span><span id="VALIDATE_YOUR_DEVICE_METADATA"></span>验证你的设备元数据


可以使用 **设备元数据创作向导** 来验证 UWP 设备应用或设备的设备元数据。

**使用设备元数据创作向导验证设备元数据**

1.  从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin x86 中打开 **设备元数据创作向导** \\ \\ \\ \\ 。
2.  单击 " **验证元数据**"。
3.  在 " **选择要验证的元数据包** " 页上，执行以下操作：
    -   在 **设备元数据包** 标题下，单击 " **浏览** " 以选择你的 devicemanifest 文件，如果你已在本地部署设备元数据，请单击 " **从本地元数据存储中选择** "。
    -   如果要针对 UWP 应用进行验证，请选中 " **根据 uwp 设备应用验证设备元数据包** " 复选框，然后单击 " **浏览** " 以选择 Microsoft Store 应用包 ( .appx) "。
    -   如果要针对某个设备进行验证，请选中 " **对设备验证设备元数据包"** 复选框，单击 " **从设备中选择**"，选择你的设备，然后单击 **"确定"。**

4.  单击 **“验证”** 。
5.  验证完成后，可以保存报表。 单击“关闭”  。
    **警告**  你可能会在验证报告中收到一个错误，指出 "应用包中 storeManifest.xml 之间的体验 ID 与设备元数据文件中的 packageInfo.xml 不匹配。" 可以放心忽略此消息。

     

## <a name="span-idnext_stepspanspan-idnext_stepspanspan-idnext_stepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤5：提交应用](step-5--submit-the-app.md)

 

 





