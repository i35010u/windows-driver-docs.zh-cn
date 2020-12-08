---
title: 步骤2为 UWP 设备应用创建设备元数据
description: 本主题介绍如何使用设备元数据创作向导来创建将 UWP 设备应用与设备关联的新设备元数据。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7577c6404e1a66d4fdaa0a2d2fc55ea912e6bb10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802669"
---
# <a name="step-2-create-device-metadata-for-your-uwp-device-app"></a>步骤2：创建 UWP 设备应用的设备元数据

![设备应用工作流，步骤2](images/2-device-app-workflow.png)

本主题介绍如何使用 **设备元数据创作向导** 来创建将 UWP 设备应用与设备关联的新设备元数据。 向导还可以创建一个 **StoreManfest.xml** 文件，该文件可能需要在下一步中添加到应用中。

UWP 设备应用是一种特殊类型的 UWP 应用，设备制造商可以创建它来充当其内部或外围设备。 通过使用设备元数据，设备应用可以运行特权操作并在设备接通电源时自动安装。 有关 UWP 设备应用的详细信息，请参阅 " [满足 uwp 设备应用](meet-uwp-device-apps.md)"。

**注意**  本主题是分步序列的一部分。 有关简介，请参阅 [构建 UWP 设备应用循序渐进](build-a-uwp-device-app-step-by-step.md) 。

## <a name="before-you-begin"></a>在开始之前

若要使用 **设备元数据创作向导**，在完成本主题中的步骤之前，必须安装 Microsoft Visual Studio Professional、Microsoft Visual Studio Ultimate 或 [独立的 SDK for Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)。 为 Windows 安装 Microsoft Visual Studio Express 会安装不包括向导的 SDK 版本。

## <a name="create-new-device-metadata"></a>创建新的设备元数据

**设备元数据创作向导** 用于创建新的设备元数据。

### <a name="to-create-new-device-metadata"></a>创建新的设备元数据

1. 双击DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin X86 启动 **设备元数据创作向导** \\ \\ \\ \\ 。 ****

2. 单击 " **新设备元数据**"。

3. 在 " **选择元数据包类型** " 页上，单击 " **UWP 设备应用元数据**"，然后单击 " **下一步**"。

4. 在 " **选择设备类别** " 页上，选择应分配给设备的设备类别。 一个设备可以属于多个设备类别，但只能分配一个主类别。 单击 **“下一步”** 。

5. 在 " **指定区域设置** " 页上，选择至少一个应与设备元数据包关联的区域设置。 你还可以设置在计算机上不能使用特定于区域设置的包时使用的默认区域设置。 单击 **“下一步”** 。

6. 在 " **描述设备** " 页上，输入向插入设备的最终用户显示的信息。 每个区域设置都需要一个模型名称和制造商。

7. 在 " **指定硬件信息** " 页上，至少添加一个硬件 id 和一个模型 id。 硬件 ID 应该包含公司的供应商 ID。 模型 ID 是一个 GUID，推荐使用此方法将设备元数据与支持模型 ID 的设备关联。 单击 **“下一步”** 。

8. 在 " **指定 UWP 设备应用信息** " 页上：

   - 如果要为设备应用启用 [自动安装](auto-install-for-uwp-device-apps.md) ，或扩展 [照相机](uwp-device-apps-for-webcams.md) 或 [打印机](uwp-device-apps-for-printers.md) 体验 (需要自动安装) ，请在 " **UWP 设备应用** " 框中输入 Microsoft Store 应用信息。 单击 " **导入 UWP 应用程序清单文件** " 以自动输入 **包名称**、 **发布者名称** 和 **UWP 应用 ID**。

     > [!Warning]
     > 请注意，在安装应用时，自动安装功能不会向用户提供通知。 某些用户可能会发现这种体验令人费解，并使应用程序成为不良评级。

   - 如果你的应用正在注册打印机通知，请填写 **通知处理程序** 框。 在 " **事件 ID**" 中，输入打印事件处理程序的名称。 在 " **事件资产**" 中，输入代码所在的文件的名称。

   - 如果要将应用指定为特权应用，请在 " **特权应用程序** " 框中输入该信息。 特许的应用程序指定可让 UWP 设备应用执行 [设备更新](device-sync-and-update-for-uwp-device-apps.md)，例如固件更新。 它还允许 Oem 和组件供应商为 [内部设备](uwp-device-apps-for-specialized-devices.md)开发应用程序。

9. 完成指定任何自动安装和特权应用的详细信息后，单击 "**下一步**"

10. 在 " **指定 Windows 设置** " 页上，你可以配置设备在断开连接时是否显示在设备管理器，以及设备应如何响应自动播放激活。

    如果要将应用指定为设备的默认自动播放处理程序，请在 "**自动播放处理程序**" 框中选择 "**使用 UWP 设备应用**"。 你可以选择任何 UWP 应用或 UWP 设备应用，但该应用必须处理设备的自动播放激活并在应用包清单中指定相应的体验 ID (如) 的 [UWP 设备应用自动播放](autoplay-for-uwp-device-apps.md) 中所述。

    - **包名称**：在应用包清单中，这是 Identity 元素的 name 属性。

    - **发布者名称**：在应用包清单中，这是 Identity 元素的发布服务器特性。

    - **应用 ID**：在应用包清单中，这是应用程序元素的 ID 属性。

    - **Verb**：这是自动播放激活的标识符。 你的应用程序将使用它来确定激活是否来自你的设备。 可以将任何值用于谓词设置，但 **open** 除外。

    - **自动播放事件类型**：将其保留为 **设备**。 在设备元数据中，向导将自动指定与 UWP 设备应用关联的体验 ID。

    如果想让其他应用充当设备的自动播放处理程序，请选择 " **为已注册的应用程序启用自动播放**"。

    有关自动播放的详细信息，请参阅 [UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)。

11. 准备好继续时，单击 " **下一步**"。

12. 在 " **查看设备元数据包** " 页上，确保所有设置都正确。 如果希望此设备元数据包在本地元数据存储中可用，请选中 " **将设备元数据包复制到本地计算机上的元数据存储区** " 复选框，然后单击 " **保存**"。

13. 如果已准备好提交设备元数据包，或者需要对其进行编辑，则必须使用 devicemanifest-ms 文件。 Devicemetadata-ms 文件应仅用于测试设备元数据。

## <a name="next-step"></a>后续步骤

[步骤3：将体验 ID 添加到应用](step-3--add-an-experience-id-to-the-app.md)

## <a name="related-topics"></a>相关主题

[构建 UWP 设备应用](the-workflow.md)

[UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)

[适用于内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)
