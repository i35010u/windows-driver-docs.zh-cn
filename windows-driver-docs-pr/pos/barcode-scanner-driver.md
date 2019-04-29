---
title: 条形码扫描仪驱动程序示例
description: 条形码扫描程序驱动程序示例演示如何创建条形码扫描程序的通用驱动程序，旨在以用作创建新的条形码扫描程序驱动程序的模板。
ms.assetid: 29374910-AF1A-40E4-8A5D-B48D7D2FD5D8
ms.date: 09/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f4d5b830b25bfc9a010829d28b1ca1056d8b25c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358691"
---
# <a name="barcode-scanner-driver-sample"></a>条形码扫描仪驱动程序示例

条形码扫描程序驱动程序示例演示如何创建条形码扫描程序的通用驱动程序，旨在以用作创建新的条形码扫描程序驱动程序的模板。 此示例使用用户模式驱动程序框架 (UMDF) 2.0，并演示了基本功能，如声明进行独占访问设备。 可以编译示例驱动程序，并且将其部署到 x86、amd64 和 ARM 平台。 有关通用驱动程序的详细信息，请转到[通用 Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)。

## <a name="requirements"></a>要求

-   Windows 10
-   [Microsoft Visual Studio 2015](https://go.microsoft.com/fwlink/p/?LinkId=533470) （任何版本）
-   [Windows 驱动程序工具包 (WDK) 10](https://go.microsoft.com/fwlink/p/?LinkId=733614)

Windows 软件开发工具包 (SDK) 10 也是必需的但这 Microsoft Visual Studio 2015 的一部分安装。

> [!NOTE]
> 示例驱动程序不需要任何磁条阅读器硬件函数，因为它对软件设备进行操作。 如果你想要使用该示例使用的硬件设备，你仍可以通过将设备的硬件 ID 添加到 INF 文件使用该驱动程序。

## <a name="download-and-extract-the-sample"></a>下载并解压缩示例

从 Windows 10 开始，Windows 驱动程序示例是 GitHub 上提供，可以从下载[Windows 驱动程序示例存储库项目页](https://go.microsoft.com/fwlink/p/?LinkId=616507)。

1.  下载**Windows 驱动程序示例 master.zip**从[GitHub](https://go.microsoft.com/fwlink/p/?LinkID=623296)。 此文件包含所有的 Windows 驱动程序示例。
2.  提取**Windows 驱动程序示例 master.zip**到开发计算机上所选的位置。 此位置将作为称为*&lt;示例\_根&gt;* 这篇文章的其余所有部分。

## <a name="open-the-driver-solution-in-visual-studio"></a>在 Visual Studio 中打开驱动程序解决方案

1.  在 Windows 资源管理器，导航到`<sample_root>\pos\drivers\barcodescanner\`文件夹。
2.  双击解决方案文件**BarcodeScanner.sln**以使用 Visual Studio 2015 中打开的解决方案。
3.  因此当您打开解决方案时，可能会看到一条安全警告，是从 Internet 下载项目 zip 文件。 如果需要，请单击**确定**完成加载项目。
4.  在 Visual Studio 中，找到**解决方案资源管理器**。 如果这是未打开，选择**解决方案资源管理器**从**视图**菜单。 在中**解决方案资源管理器**，可以看到该项目，并且它的源文件包含。

## <a name="build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例

1.  从*标准*在 Visual Studio 中，选择工具栏*解决方案平台*匹配你的操作系统平台。 例如，如果使用 Windows 的 64 位版本，则选择 x64。
    > [!NOTE]
    > 如果面向 ARM 平台，你需要使用配置管理器将 ARM 添加到目标的列表。

     
2.  选择**生成解决方案**从**生成**菜单。

## <a name="install-the-driver"></a>安装驱动程序


1.  生成时，该驱动程序的签名时使用测试证书。 若要安装驱动程序进行测试，您需要更改启动配置为允许驱动程序的证书签名的测试加载。 若要更改该设置，打开提升的命令提示符并输入命令：

    `bcdedit.exe /set TESTSIGNING on`

2.  重新启动计算机。
    **请注意**  不需要有以前启用测试签名，如果重新启动。

     

3.  从提升的命令提示符，导航到您的项目已生成的文件夹。 如果创建 x64 调试版本，此文件夹将为`<project_root>\x64\Debug\SampleBarcodeScannerDrv`。

    在该文件夹中，将看到以下文件：

    | 文件                        | 描述                                                                  |
    |-----------------------------|------------------------------------------------------------------------------|
    | SampleBarcodeScannerDrv.dll | 驱动程序文件中。                                                             |
    | SampleBarcodeScannerDrv.inf | 一个包含所需安装驱动程序信息的 INF 文件。          |
    | samplebarcodescannerdrv.cat | 签名的编录文件，可作为整个程序包的签名。 |

     

4.  标识与你 OS 和驱动程序的平台匹配设备控制台实用程序 (devcon.exe) 的路径。 X64 版在默认位置`C:\Program Files (x86)\Windows Kits\10\Tools\x64`。
5.  键入以下命令，用&lt;devcon\_路径&gt;替换为你在上一步中找到的 devcon.exe 文件的路径。

    `"<devcon_path>\devcon.exe" install SampleBarcodeScannerDrv.inf Root\SampleBarcodeScannerDrv`

6.  你将看到**Windows 安全**对话框，通知您无法验证该驱动程序的发布者。 这是因为该驱动程序已使用测试证书进行签名。 单击**是否仍要安装该驱动程序软件**。 稍后，你将看到确认您的驱动程序正确安装。

如果设备控制台实用程序不能安装驱动程序，确认你已使用一个与你的当前 OS 平台和驱动程序的平台匹配。

## <a name="view-the-device-in-device-manager"></a>查看设备管理器中的设备

1.  打开“设备管理器”。 这可以完成许多方面，但如果您仍在命令提示符然后键入`devmgmt`。
2.  在设备管理器中，选择**依类型排序设备**从**视图**菜单。
3.  将设备列入**示例**节点。
