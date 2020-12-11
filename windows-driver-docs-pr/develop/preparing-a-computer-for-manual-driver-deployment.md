---
title: 准备一台用于手动部署驱动程序的计算机
description: 介绍在手动部署驱动程序之前如何准备目标计算机。
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: c5a2615f79517049e9894f81fe0b4b459369346c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824645"
---
# <a name="preparing-a-computer-for-manual-driver-deployment"></a>准备一台用于手动部署驱动程序的计算机

你可以自动或手动部署驱动程序。 无论哪种情况，都需要先准备目标计算机。 在此处，我们将介绍在选择手动部署驱动程序时如何准备目标计算机。

通常，安装和测试驱动程序的计算机与开发和生成驱动程序包的计算机是分开的。 生成驱动程序的计算机称为“主计算机”  ，而安装和测试驱动程序的计算机则称为“目标计算机”  或“测试计算机”  。 将驱动程序包移至目标计算机并安装驱动程序的过程称为“部署驱动程序”  。

1.  在目标计算机上，以管理员身份打开“命令提示符”窗口。 输入“bcdedit /set TESTSIGNING ON”  。 重新启动目标计算机。
2.  将 [DevCon](../devtest/devcon.md) 工具复制到目标计算机上的某个文件夹（例如，c:\\Tools）。 DevCon 工具包括在 Windows 驱动程序工具包 (WDK) 中。 可以在 Tools 目录下找到它（例如，C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe）。
3.  创建或获取一个可安装在目标计算机上的证书 (.cer) 文件。 例如，在生成其中一个 WDK 示例驱动程序时，生成过程会创建一个证书 (.cer) 文件。 证书文件的位置各不相同，具体取决于你指定的配置和平台。 例如，如果你的配置为“Win7 调试”且平台为 x64，则证书文件位于 C++\\x64\\Win7Debug 下的解决方案文件夹中。
4.  将证书文件复制到目标计算机上的某个文件夹中（例如，c:\\Certificates）。
5.  在目标计算机上，选择并按住（或右键单击）证书文件，然后选择“安装”。 按照安装向导进行操作。

生成其中一个 WDK 驱动程序示例时，生成过程将会创建一个测试签名证书。 只需安装一次测试签名证书。 如果已安装 WDK 驱动程序示例的证书，则无需再次安装证书即可安装其他驱动程序示例。
