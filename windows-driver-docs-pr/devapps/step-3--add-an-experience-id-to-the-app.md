---
title: 步骤3将体验 ID 添加到 Microsoft Store 设备应用
description: 本主题介绍如何将体验 ID 添加到 UWP 设备应用。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b600c79fc9d591d3165302216a0f2b99e469a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815171"
---
# <a name="step-3-add-an-experience-id-to-the-microsoft-store-device-app"></a>步骤3：将体验 ID 添加到 Microsoft Store 设备应用


![设备应用工作流，步骤3](images/3-device-app-workflow.png)

本主题介绍如何将体验 ID 添加到 UWP 设备应用。 *体验 ID* 是一个 GUID，用于唯一标识设备元数据包;如果你的应用程序已配置为自动安装，则这是必需的，因为适用于打印机和 [照相机](uwp-device-apps-for-webcams.md)的 [UWP 设备应用](uwp-device-apps-for-printers.md)。

**提示**  如果你的应用被指定为特权应用并且未配置为自动安装，则可以跳过此步骤。

 

UWP 设备应用是一种特殊类型的 UWP 应用，设备制造商可以创建它来充当其内部或外围设备。 通过使用设备元数据，设备应用可以运行特权操作并在设备接通电源时自动安装。 有关 UWP 设备应用的详细信息，请参阅 " [满足 uwp 设备应用](meet-uwp-device-apps.md)"。

**注意**  本主题是分步序列的一部分。 有关简介，请参阅 [构建 UWP 设备应用循序渐进](build-a-uwp-device-app-step-by-step.md) 。

 

## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前


此步骤需要在 [上一步](step-2--create-device-metadata.md)中创建的 StoreManifest.xml 文件。 StoreManifest.xml 文件指定体验 ID。

## <a name="span-idadd_storemanifestxml_to_your_projectspanspan-idadd_storemanifestxml_to_your_projectspanadd-storemanifestxml-to-your-project"></a><span id="add_storemanifest.xml_to_your_project"></span><span id="ADD_STOREMANIFEST.XML_TO_YOUR_PROJECT"></span>将 StoreManifest.xml 添加到项目


StoreManifest.xml 文件中指定了体验 ID。 此 ID 将应用链接到设备元数据。

**重要说明**  
StoreManifest.xml 文件必须存储在应用项目的根文件夹中，而不是存储在解决方案的根文件夹中。

 

**将 StoreManifest.xml 添加到项目中**

1.  在 **解决方案资源管理器** 中，右键单击项目，然后选择 " **添加 &gt; 现有项**"。
2.  在 " **添加现有项** " 对话框中，选择你在 [上一步](step-2--create-device-metadata.md)中创建的 StoreManifest.xml 文件。
3.  将 StoreManifest.xml 文件添加到项目后，请查看该文件的属性。 右键单击 **StoreManifest.xml** 文件，然后选择 " **属性**"。 这将突出显示 " **属性** " 窗口。
4.  在 " **属性** " 窗口中，确保 " **生成操作** " 属性等于 " **内容** "，并确保 " **复制到输出目录** " 属性等于 " **不复制**"。

有关 StoreManifest.xml 文件的详细信息，请参阅 [storemanifest.xml 架构参考](/uwp/schemas/storemanifest/storemanifestschema2010/schema-root)。

## <a name="span-idnext_stepspanspan-idnext_stepspanspan-idnext_stepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤4：测试设备元数据](step-4--test-device-metadata.md)

 

