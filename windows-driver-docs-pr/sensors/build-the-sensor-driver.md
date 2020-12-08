---
title: 构建传感器驱动程序
description: 本主题说明如何构建 ADXL345 加速感应器的示例传感器驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef146255e94d3581bfce71a1456ff9351b50372d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831065"
---
# <a name="build-the-sensor-driver"></a>构建传感器驱动程序


本主题说明如何构建 ADXL345 加速感应器的示例传感器驱动程序。

## <a name="download-the-driver-files"></a>下载驱动程序文件


导航到 GitHub 上的 [Microsoft/Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) 站点，然后执行以下任务以下载并构建示例传感器驱动程序。 本主题中的练习假设您的开发计算机上安装了 Microsoft Visual Studio 2015。 否则，请访问 [此下载网站](https://visualstudio.microsoft.com/downloads/) ，了解有关如何下载 Microsoft Visual Studio 的副本的信息。

1. 在开发计算机上为要下载的示例传感器驱动程序文件创建一个文件夹。

2. 在 [Microsoft/Windows-driver](https://github.com/Microsoft/Windows-driver-samples) 站点上的右侧窗格中，单击 " **下载 ZIP**"。

3. 在屏幕底部的 "文件保存" 提示符下，单击 " **保存**"。 将下载 zip 文件并将其保存到默认位置，即 " **下载** " 文件夹。

4. 导航到 " **下载** " 文件夹，找到并右键单击名为 " *Windows-驱动程序-示例-主* 文件夹" 的文件夹。 选择 " **全部提取**"。 请注意，此主 zip 文件包含许多不同技术的驱动程序示例，而不仅仅适用于传感器。

5. 在 " **提取压缩的 (Zipped) 文件夹** " 窗口中，单击 " **提取**"。 文件将被提取到 "**下载**" 文件夹中也称为 " **Windows-驱动** 程序-示例" 的文件夹中。 请注意，这是一个很大的文件，可能需要几分钟才能提取所有文件。

6. 打开 " **Windows-驱动程序-示例-主** 文件夹"，然后找到并打开 " **传感器** " 文件夹。

7. 在 " **传感器** " 文件夹中，打开 **ADXL345Acc** 文件夹，复制此文件夹中的所有文件，并将其粘贴到 **步骤 1** 中创建的项目文件夹中。

## <a name="build-the-driver-in-visual-studio"></a>在 Visual Studio 中生成驱动程序


1. 在 Visual Studio 中，单击 " **文件**" " &gt; **打开** &gt; **项目/解决方案**"。

2. 在 " **打开项目** " 窗口中，导航到项目文件夹，并找到传感器示例的内容。 然后打开 " **ADXL345Acc**"，然后双击 " *ADXL345Acc* " 解决方案文件。

3. 单击 " **生成**" "生成 &gt; **解决方案** "，生成 ADXL345 加速感应的示例驱动程序。

4. 完成生成后，检查 " **输出** " 窗口，确保没有生成错误。 如果有错误，请解决这些错误，然后单击 " **生成** &gt; **重新生成解决方案**"。

5. 使用 **文件资源管理器**，导航到项目文件夹，然后打开由生成过程创建的 " **调试** " 文件夹。

6. 在 **调试** 中，打开 **ADXL345Acc** 文件夹，并检查以确保可以看到以下三个文件：

-   *adxl345acc.cat* -安全目录文件。

-   *ADXL345Acc.dll* -应用程序扩展。 这是实际的传感器驱动程序。

-   *ADXL345Acc* -安装信息文件。

7. 将这三个文件从 **ADXL345Acc** 文件夹复制到闪存驱动器上，然后按照 [安装传感器驱动程序](install-the-sensor-driver.md) 中的步骤来安装 ADXL345 加速感应器的示例传感器驱动程序。
 

 




