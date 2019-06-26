---
title: 生成传感器驱动程序
description: 本主题演示如何生成 ADXL345 加速感应器的示例传感器驱动程序。
ms.assetid: F9D8D124-DAD6-4779-9F03-B1743BADC31A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97efc50cef8b4beda312b448dd2d904210053a76
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393346"
---
# <a name="build-the-sensor-driver"></a>生成传感器驱动程序


本主题演示如何生成 ADXL345 加速感应器的示例传感器驱动程序。

## <a name="download-the-driver-files"></a>下载驱动程序文件


导航到[Microsoft / Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)在 GitHub 上的站点，请执行以下任务来下载和生成示例传感器驱动程序。 本主题中的练习假定你已在开发计算机上安装 Microsoft Visual Studio 2015。 如果没有，请访问[此下载站点](https://visualstudio.microsoft.com/downloads/)有关如何下载 Microsoft Visual Studio 的副本的信息。

1. 将下载的示例传感器驱动程序文件在开发计算机上创建一个文件夹。

2. 在右侧窗格中[Microsoft / Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)站点中，单击**下载 ZIP**。

3. 在屏幕底部提示保存文件，单击**保存**。 将下载的 zip 文件，并将其保存到默认位置，即**下载**文件夹。

4. 导航到**下载**文件夹，然后找到并右键单击文件夹，名为*母版 Windows 驱动程序示例*。 选择**提取所有**。 请注意，此主 zip 文件包含许多不同的技术，而不只是传感器驱动程序示例。

5. 在中**提取压缩 (Zipped) 文件夹**窗口中，单击**提取**。 文件将被提取到文件夹，也称为**Windows 驱动程序示例主**，在**下载**文件夹。 请注意，这是一个大型文件，它可能需要几分钟才能提取所有文件。

6. 打开**Windows 驱动程序示例主**文件夹，然后查找并打开**传感器**文件夹。

7. 在**传感器**文件夹中，打开**ADXL345Acc**文件夹，并在此文件夹中的所有文件都复制并粘贴到项目文件夹中创建**第 1 步**。

## <a name="build-the-driver-in-visual-studio"></a>生成 Visual Studio 中的驱动程序


1. 在 Visual Studio 中，单击**文件** &gt; **打开** &gt; **项目/解决方案**。

2. 在中**打开项目**窗口中，导航到项目文件夹，并查找的传感器示例内容。 然后打开**ADXL345Acc**，然后双击*ADXL345Acc*解决方案文件。

3. 单击**构建** &gt; **生成解决方案**生成 ADXL345 加速感应器的示例驱动程序。

4. 生成完成后，检查**输出**窗口以确保没有生成错误。 如果有错误，解决这些冲突，然后依次**构建** &gt; **重新生成解决方案**。

5. 使用**文件资源管理器**，导航到项目文件夹，然后打开**调试**生成过程创建的文件夹。

6. 在中**调试**，打开**ADXL345Acc**文件夹，然后检查以确保可以看到以下三个文件：

-   *adxl345acc.cat* -安全目录文件。

-   *ADXL345Acc.dll* -应用程序扩展。 这是实际的传感器驱动程序。

-   *ADXL345Acc.inf* -安装信息文件。

7. 将从这三个文件复制**ADXL345Acc**文件夹中的拖到闪存驱动器，然后按照中的步骤[安装传感器驱动程序](install-the-sensor-driver.md)安装 ADXL345 加速感应器的示例传感器驱动程序。
 

 




