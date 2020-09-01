---
title: 磁条读取器驱动程序示例
description: 此示例演示如何为磁条纹读取器创建通用驱动程序，并将其用作创建新驱动程序的模板。
ms.assetid: 92A8C116-F71F-4A74-A453-44C14297BCDD
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff77c0e4b73657e7415db37ef1f44b96f7cbc9f5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185777"
---
# <a name="magnetic-stripe-reader-driver-sample"></a>磁条读取器驱动程序示例

磁条读取器驱动程序示例演示如何为磁条纹读取器创建通用驱动程序，并将其用作创建新驱动程序的模板。 该示例使用用户模式驱动程序框架 (UMDF) 2.0，并演示了基本功能，如声明设备以进行独占访问。 示例驱动程序可以在 x86、amd64 和 ARM 平台上编译和部署。

## <a name="requirements"></a>要求

- Windows 10

- [Microsoft Visual Studio](https://visualstudio.microsoft.com) (任何版本) 

- [Windows 驱动程序工具包 (WDK) 10](../download-the-wdk.md)

Windows 软件开发工具包 (SDK) 10 也是必需的，但它作为 Microsoft Visual Studio 的一部分进行安装。

> [!NOTE]
> 示例驱动程序不需要任何磁条读取器硬件即可正常运行，因为它在软件设备上运行。 如果你有要用于此示例的硬件设备，仍可通过将设备的硬件 ID 添加到 INF 文件来使用该驱动程序。

## <a name="download-and-extract-the-sample"></a>下载并提取示例

GitHub 上提供了 [Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples) 。

1. 下载 [**Windows-driver-samples-master.zip**](https://github.com/microsoft/Windows-driver-samples/archive/master.zip)。 此文件包含 (WDK) 示例的所有 Windows 驱动程序工具包。

1. 将 **Windows-driver-samples-master.zip** 提取到你选择的开发计算机上的位置。 此位置将在 `<sample_root>` 本文的其余部分中称为。

## <a name="open-the-driver-solution-in-visual-studio"></a>在 Visual Studio 中打开驱动程序解决方案

1. 在 Windows 资源管理器中，导航到 `<sample_root>\pos\drivers\MagneticStripeReader` 文件夹。

1. 双击解决方案文件 **MagneticStripeReader** ，以通过 Visual Studio 打开解决方案。

1. 已从 Internet 下载项目 zip 文件，因此打开解决方案时可能会看到安全警告。 如果执行此操作，请单击 **"确定"** 完成项目加载。

1. 在 Visual Studio 中，找到 **解决方案资源管理器**。 如果尚未打开，则从 "**视图**" 菜单中选择 "**解决方案资源管理器**"。 在 **解决方案资源管理器**中，可以看到项目及其包含的源文件。

## <a name="build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例

1. 在 Visual Studio 的 " *标准* " 工具栏中，选择与你的操作系统平台相匹配的 *解决方案平台* 。 例如，如果使用的是64位版本的 Windows，则选择 "x64"。

    > [!NOTE]
    > 如果面向 ARM 平台，则需要使用配置管理器将 ARM 添加到目标列表。

1. 从 "**生成**" 菜单中选择 "**生成解决方案**"。

## <a name="install-the-driver"></a>安装驱动程序

1. 生成时，驱动程序已使用测试证书进行签名。 若要安装用于测试的驱动程序，需要更改启动配置，以允许加载使用测试证书签名的驱动程序。 若要更改设置，请打开提升的命令提示符并输入以下命令：

    `bcdedit.exe /set TESTSIGNING on`

1. 重启计算机。

    > [!NOTE]
    > 如果以前启用了测试签名，则不需要重新启动。

1. 在提升的命令提示符下，导航到生成项目的文件夹。 如果创建了 x64 调试版本，则此文件夹将为 `<project_root>\x64\Debug\SampleMagneticStripeReaderDrv` 。

    在该文件夹中，你将看到以下文件：

    | 文件                              | 说明                                                                  |
    |-----------------------------------|------------------------------------------------------------------------------|
    | SampleMagneticStripeReaderDrv.dll | 驱动程序文件。                                                             |
    | SampleMagneticStripeReaderDrv .inf | 一个 INF 文件，其中包含安装驱动程序所需的信息。          |
    | samplemagneticstripereaderdrv.cat | 签名目录文件，用作整个包的签名。 |

1. 标识设备控制台实用工具的路径 ( # A0) 与操作系统和驱动程序平台相匹配。 X64 版本的默认位置是 `C:\Program Files (x86)\Windows Kits\10\Tools\x64` 。

1. 键入以下命令，将 &lt; devcon \_ 路径替换 &gt; 为你在上一步中找到的 devcon.exe 文件的路径。

    `"<devcon_path>\devcon.exe" install SampleMagneticStripeReaderDrv.inf Root\SampleMagneticStripeReaderDrv`

1. 你将看到 " **Windows 安全** " 对话框，通知你无法验证驱动程序的发布者。 这是因为已使用测试证书对驱动程序进行签名。 单击 " **仍安装此驱动程序软件**"。 稍后，你将看到有关驱动程序安装正确的确认。

如果设备控制台实用工具无法安装该驱动程序，请确认你使用的是与当前操作系统平台和驱动程序平台相匹配的设备。

## <a name="view-the-device-in-device-manager"></a>在设备管理器中查看设备

1. 打开“设备管理器”。 这可以通过多种方式完成，但如果仍处于命令提示符下，请键入 `devmgmt` 。

1. 在设备管理器中，从 "**视图**" 菜单中选择 "**设备类型**"。

1. 你的设备将在 " **示例** " 节点下列出。