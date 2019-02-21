---
title: UWP 设备应用程序的步骤 2 创建设备元数据
description: 本主题介绍如何使用设备元数据创建向导来创建新的设备元数据将 UWP 设备应用与设备相关联。
ms.assetid: 61A3AE1B-2256-4034-AE9F-86E6900D9093
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f17cc44c5827959cbe3c2fd1306cb16d672ef25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542741"
---
# <a name="step-2-create-device-metadata-for-your-uwp-device-app"></a>步骤 2：创建 UWP 设备应用的设备元数据

![设备应用工作流，第 2 步](images/2-device-app-workflow.png)

本主题介绍如何使用**设备元数据创建向导**若要创建新的设备元数据将 UWP 设备应用与设备相关联。 该向导还可以创建**StoreManfest.xml**可能需要添加到下一步中的应用的文件。

UWP 设备应用程序是一种特殊的设备制造商创建作为其内部或外围设备的配套的 UWP 应用。 使用设备元数据，设备应用程序可以运行特权的操作，并在插入设备时，自动安装。 有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**请注意**本主题是分步系列的一部分。 请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)引入。

## <a name="before-you-begin"></a>开始之前

若要使用**设备元数据创建向导**，则必须安装 Microsoft Visual Studio Professional，Microsoft Visual Studio Ultimate，或[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)，完成之前本主题中的步骤。 安装 Microsoft Visual Studio Express 的 Windows 安装不包括在向导的 sdk 版本。

## <a name="create-new-device-metadata"></a>创建新的设备元数据

**设备元数据创建向导**用于创建新的设备元数据。

### <a name="to-create-new-device-metadata"></a>若要创建新的设备元数据

1. 启动**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**。

2. 单击**新的设备元数据**。

3. 上**选择元数据的包类型**页上，单击**UWP 设备应用元数据**，然后单击**下一步**。

4. 上**选择设备类别**页上，选择应分配给你的设备的设备类别。 设备可以属于多个设备类别，但只有一个主类别可以分配。 单击“下一步” 。

5. 上**指定的区域设置**页上，选择应与设备元数据包相关联的至少一个区域设置。 此外可以设置特定于区域设置的包不在计算机上可用时使用的默认区域设置。 单击“下一步” 。

6. 上**将该设备描述**页上，输入向将设备插入的最终用户显示的信息。 需要为每个区域设置模型名称和制造商。

7. 上**指定的硬件信息**页上，添加至少一个硬件 ID 和一个模型 id。 硬件 ID 应为你的公司包括供应商 ID。 模型 ID 是 GUID，并且是支持模型 id。 设备相关联的设备元数据的推荐的方法 单击“下一步” 。

8. 上**指定 UWP 设备应用信息**页：

   - 如果你想要启用[自动安装](auto-install-for-uwp-device-apps.md)为你的设备应用，或扩展[照相机](uwp-device-apps-for-webcams.md)或[打印机](uwp-device-apps-for-printers.md)体验 （需要自动安装） 中，输入中的 Microsoft Store 应用程序信息**UWP 设备应用**框。 单击**导入 UWP 应用程序清单文件**自动输入**包名称**，**发布服务器的名称**，以及**UWP 应用程序 ID**。

     > [!Warning]
     > 请务必要考虑，自动安装功能不提供通知给用户安装应用。 有些用户可能发现这种体验让人困惑和令人沮丧，并为您的应用程序提供错误评级。

   - 如果您的应用程序注册的打印机通知，填写**通知处理程序**框。 在中**事件 ID**，输入打印事件处理程序的名称。 在中**事件资产**，输入该代码所在的位置的文件的名称。

   - 如果你想要指定您的应用程序为特权的应用，输入该信息**特权应用程序**框。 特权的应用指定的允许执行的 UWP 设备应用程序[设备更新](device-sync-and-update-for-uwp-device-apps.md)，例如固件更新。 它还允许 Oem 和组件供应商开发适用于应用程序[内部设备](uwp-device-apps-for-specialized-devices.md)。

9. 在完成指定的任何自动安装和特权的应用的详细信息，请单击**下一步**

10. 上**指定的 Windows 设置**页上，可以配置该设备显示在设备管理器断开连接时，设备应如何响应为自动播放激活。

    如果你想要指定应用为你的设备，选择的默认自动播放处理程序**使用 UWP 设备应用**中**自动播放处理程序**框。 您可以选择任何 UWP 应用或 UWP 设备应用，但该应用程序必须处理你的设备的自动播放激活，并指定相应体验应用包清单中的 ID (如中所述[UWP 设备应用程序的自动播放](autoplay-for-uwp-device-apps.md))。

    - **包名称**:在应用包清单中，这是标识元素的 Name 属性。

    - **发布者名称**:在应用包清单中，这是标识元素的发布服务器属性。

    - **应用程序 ID**:在应用包清单中，这是应用程序元素的 ID 属性。

    - **谓词**:这是自动播放激活的标识符。 您的应用程序将使用它来确定是否激活来自你的设备。 可用于任何值对于谓词设置中，除**打开**，这保留的。

    - **自动播放事件类型**:保留原样**设备**。 设备元数据，在该向导将自动指定与 UWP 设备应用程序关联的体验 ID。

    如果你想要让自动播放处理程序为你的设备，选择充当其他应用**启用的已注册应用的自动播放**。

    有关自动播放的详细信息，请参阅[UWP 设备应用程序的自动播放](autoplay-for-uwp-device-apps.md)。

11. 准备好继续时，单击**下一步**。

12. 上**查看设备元数据包**页上，请确保所有设置正确。 如果您希望此设备元数据包，可在本地元数据存储区中，选择**复制到本地计算机上的元数据存储设备元数据包**复选框，然后依次**保存**.

13. 如果你已准备好提交设备元数据包，或者如果您需要对其进行编辑，必须使用.devicemanifest ms 文件。 .Devicemetadata ms 文件应仅用于测试本地设备元数据。

## <a name="next-step"></a>下一步

[步骤 3:向应用添加体验 ID](step-3--add-an-experience-id-to-the-app.md)

## <a name="related-topics"></a>相关主题

[构建 UWP 设备应用程序](the-workflow.md)

[设备同步和 UWP 的设备应用程序的更新](device-sync-and-update-for-uwp-device-apps.md)

[UWP 应用的内部设备的设备应用程序](uwp-device-apps-for-specialized-devices.md)
