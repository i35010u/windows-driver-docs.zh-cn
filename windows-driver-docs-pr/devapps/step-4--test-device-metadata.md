---
title: 步骤 4 测试 UWP 设备应用的设备元数据
description: 本主题介绍如何测试设备元数据为 UWP 设备应用本地之前将其提交至 Windows 开发人员中心仪表板。
ms.assetid: C1DA36DE-DB89-4A2A-8B9F-DF2A279D3EDD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac63ded86f4c48343fd3073d3eb55d3bdc35984a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567717"
---
# <a name="step-4-test-the-device-metadata-for-your-uwp-device-app"></a>步骤 4：测试 UWP 设备应用的设备元数据


![设备应用工作流，步骤 4](images/4-device-app-workflow.png)

本主题介绍如何测试设备元数据为 UWP 设备应用本地之前将其提交至 Windows 开发人员中心仪表板。

UWP 设备应用程序是一种特殊的设备制造商创建作为其内部或外围设备的配套的 UWP 应用。 使用设备元数据，设备应用程序可以运行特权的操作，并在插入设备时，自动安装。 有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**请注意**  本主题是分步系列的一部分。 请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)引入。

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前的准备工作


因此您可以测试你的设备能够正确使用它，可以部署到本地计算机上的本地设备元数据存储区的设备元数据。 设备元数据部署后，它应处理相同的方式，就像它已提交至 Windows 开发人员中心仪表板。 例如，如果为设备元数据中的设备启用了自动播放，在插入设备时，应使用自动播放处理程序。 如果更改模型或发布者名称，可以确保这些更改也体现。

测试你的设备元数据之前，应会在其中部署设备元数据的计算机上安装 Microsoft Store 应用。

## <a name="span-iddeployyourdevicemetadatalocallyspanspan-iddeployyourdevicemetadatalocallyspanspan-iddeployyourdevicemetadatalocallyspandeploy-your-device-metadata-locally"></a><span id="Deploy_your_device_metadata_locally"></span><span id="deploy_your_device_metadata_locally"></span><span id="DEPLOY_YOUR_DEVICE_METADATA_LOCALLY"></span>部署本地你设备元数据


可以测试你的设备元数据之前，必须将其部署到本地设备元数据存储区中。 可以选择执行此**复制到本地计算机上的元数据存储设备元数据包**复选框时创建的设备元数据或通过使用**设备元数据创建向导**创建设备元数据之后。

**若要使用设备元数据创建向导部署设备元数据**

1.  打开**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86。
2.  上**工具**菜单上，单击**部署元数据包**。
3.  浏览到.devicemetadata ms 文件，然后依次**打开。**
4.  如果出现用户帐户控制对话框中，单击**是**。
5.  部署设备元数据后，将看到一条消息，指出**设备元数据包已成功复制到此计算机上的本地元数据存储**。 你的设备元数据已准备好进行测试。

## <a name="span-idvalidateyourdevicemetadataspanspan-idvalidateyourdevicemetadataspanspan-idvalidateyourdevicemetadataspanvalidate-your-device-metadata"></a><span id="Validate_your_device_metadata"></span><span id="validate_your_device_metadata"></span><span id="VALIDATE_YOUR_DEVICE_METADATA"></span>验证你的设备元数据


您可以通过使用验证你针对 UWP 设备应用或设备的设备元数据**设备元数据创建向导**。

**若要使用设备元数据创建向导验证你的设备元数据**

1.  打开**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86。
2.  单击**验证元数据**。
3.  上**选择元数据包，以验证**页上，执行以下操作：
    -   下**设备元数据包**标题下方，单击**浏览**选择.devicemanifest ms 文件，或单击**从本地元数据存储中选择**如果你已部署本地你设备元数据。
    -   如果你想要验证的 UWP 应用，选择**验证针对 UWP 设备应用，设备元数据包**复选框，然后依次**浏览**选择 Microsoft Store 应用包 (.appx)。
    -   如果你想要验证设备，选择**验证针对设备的设备元数据包**复选框，单击**从设备中选择**，选择你的设备，并单击**确定。**

4.  单击 **“验证”**。
5.  完成验证后，可以保存该报表。 单击 **“关闭”**。
    **谨慎**  可能会收到指出"体验 ID 不匹配 storeManifest.xml 在应用包和设备元数据文件中的 packageInfo.xml 之间。"验证报表中的错误 你可以放心地忽略此消息。

     

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>下一步


[步骤 5：提交应用程序](step-5--submit-the-app.md)

 

 





