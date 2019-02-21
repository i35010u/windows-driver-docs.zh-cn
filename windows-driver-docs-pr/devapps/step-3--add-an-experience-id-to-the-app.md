---
title: 步骤 3 将体验 ID 添加到 Microsoft Store 设备应用
description: 本主题介绍如何将体验 ID 添加到 UWP 设备应用程序。
ms.assetid: D114C916-EADE-4C08-BF7E-628D2FA5AACC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4817a2c5c8f6395d5c0e30b47f877ab95954a435
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542836"
---
# <a name="step-3-add-an-experience-id-to-the-microsoft-store-device-app"></a>步骤 3:将体验 ID 添加到 Microsoft Store 设备应用


![设备应用工作流，步骤 3](images/3-device-app-workflow.png)

本主题介绍如何将体验 ID 添加到 UWP 设备应用程序。 *体验 ID*是一个 GUID，用于唯一标识设备元数据包，它具有需要如果您的应用程序配置为自动安装，使用这种情况[UWP 设备应用程序的打印机](uwp-device-apps-for-printers.md)和[照相机](uwp-device-apps-for-webcams.md)。

**提示**  可以跳过此步骤中，如果您的应用程序指定为特权的应用程序，并且不将其配置为自动安装。

 

UWP 设备应用程序是一种特殊的设备制造商创建作为其内部或外围设备的配套的 UWP 应用。 使用设备元数据，设备应用程序可以运行特权的操作，并在插入设备时，自动安装。 有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**请注意**  本主题是分步系列的一部分。 请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)引入。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>在开始之前


此步骤需要 StoreManifest.xml 文件中创建[上一步](step-2--create-device-metadata.md)。 StoreManifest.xml 文件指定体验 id。

## <a name="span-idaddstoremanifestxmltoyourprojectspanspan-idaddstoremanifestxmltoyourprojectspanadd-storemanifestxml-to-your-project"></a><span id="add_storemanifest.xml_to_your_project"></span><span id="ADD_STOREMANIFEST.XML_TO_YOUR_PROJECT"></span>向项目添加 StoreManifest.xml


体验 ID StoreManifest.xml 文件中指定。 此 ID 链接到的设备元数据的应用程序。

**重要**   StoreManifest.xml 文件必须存储在应用程序的项目的根文件夹而不在解决方案的根文件夹。

 

**若要将 StoreManifest.xml 添加到你的项目**

1.  在中**解决方案资源管理器**，右键单击项目，然后选择**添加&gt;现有项**。
2.  在中**添加现有项**对话框中，选择 StoreManifest.xml 文件中创建[上一步](step-2--create-device-metadata.md)。
3.  已添加到你的项目后，请查看 StoreManifest.xml 文件的属性。 右键单击**StoreManifest.xml**文件，然后选择**属性**。 它突出显示了**属性**窗口。
4.  在中**属性**窗口中，确保**生成操作**属性等于**内容**并**复制到输出目录**属性等于**不要复制**。

有关 StoreManifest.xml 文件的详细信息，请参阅[StoreManifest 架构参考](https://go.microsoft.com/fwlink/p/?LinkId=307124)。

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤 4:测试设备元数据](step-4--test-device-metadata.md)

 

 





