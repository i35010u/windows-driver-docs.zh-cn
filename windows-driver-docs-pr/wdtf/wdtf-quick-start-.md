---
title: WDTF 快速入门
description: Windows 驱动程序工具包提供了用于编写、 部署和运行测试使用 Windows 驱动程序测试框架 (WDTF) 的集成的解决方案。
ms.assetid: 77402D9A-DD21-4B7F-B052-43DB8C04EA1B
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: b076ac0ca2aba5175a03487db624b820c8aa605e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370878"
---
# <a name="wdtf-quick-start"></a>WDTF 快速入门

Windows 驱动程序工具包提供了用于编写、 部署和运行测试使用 Windows 驱动程序测试框架 (WDTF) 的集成的解决方案。 使用 WDK，可以配置用于部署、 测试和调试驱动程序的远程计算机。 在配置远程计算机时，安装 Windows 驱动程序测试框架运行时。

## <a name="installing-wdtf-runtime-library"></a>安装 WDTF 运行时库

### <a name="to-install-wdtf-runtime-library-using-visual-studio-and-the-wdk"></a>若要安装使用 Visual Studio 和 WDK WDTF 运行时库

1. 安装 Visual Studio，然后安装 WDK。

2. 配置用于测试和部署的远程计算机。 在 Visual Studio 中，在**驱动程序**菜单，依次指向**测试**，然后单击**将计算机配置...**.

3. 在配置测试计算机时，安装 Windows 驱动程序测试框架运行时。

- 有关详细信息，请参阅：

  - [将驱动程序部署到测试计算机](https://docs.microsoft.com/windows-hardware/drivers/develop/deploying-a-driver-to-a-test-computer)

  - [预配计算机以便进行驱动程序部署和测试 (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)  

### <a name="installing-the-wdtf-runtime-library-manually"></a>手动安装 WDTF 运行时库

在安装 WDK 时，也会安装 Windows 驱动程序测试框架运行时的安装包。 您需要将安装包复制到测试计算机并运行命令。 有关信息，请参阅[（备选方法） 的测试计算机上手动安装 WDTF 运行时库](https://docs.microsoft.com/windows-hardware/drivers/wdtf/wdtf-runtime-library#manually-installing-wdtf-on-a-test-computer-alternative-method)中[WDTF 运行时库](wdtf-runtime-library.md)。

## <a name="writing-tests-with-wdtf"></a>使用 WDTF 编写测试

WDK 提供了使用 WDTF 编写测试的模板。 请参阅[如何编写使用驱动程序测试模板的驱动程序测试](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-write-a-driver-test-)。 模板还可用于为你的目标设备创建 WDTF 简单 I/O 插件。 有关信息，请参阅[编写的插件为你的设备 WDTF 简单 I/O](writing-a-wdtf-simpleio-plug-in-for-your-device.md)。

## <a name="running-wdtf-tests"></a>运行 WDTF 测试

在生成你在 Visual Studio 中的驱动程序测试使用 WDTF 驱动程序测试模板，将新的测试将可供部署到测试计算机上。 默认情况下，你创建的测试将显示在测试类别**我的测试类别**中。 测试名称基于你选择的测试用例，其名称类似于**我的即插即用突然删除测试**。 在测试每个版本，测试将被覆盖，并可用于运行中轻松运行测试功能。 有关详细信息，请参阅[如何测试在运行时使用 Visual Studio 的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver-at-runtime)。
