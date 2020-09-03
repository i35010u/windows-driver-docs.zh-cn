---
title: WDTF 快速入门
description: Windows 驱动程序工具包提供了一个集成解决方案，用于编写、部署和运行使用 Windows 驱动程序测试框架 (WDTF) 的测试。
ms.assetid: 77402D9A-DD21-4B7F-B052-43DB8C04EA1B
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2139f339382bc972d1498f222017d777ab9fa5c2
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403530"
---
# <a name="wdtf-quick-start"></a>WDTF 快速入门

Windows 驱动程序工具包提供了一个集成解决方案，用于编写、部署和运行使用 Windows 驱动程序测试框架 (WDTF) 的测试。 使用 WDK，你可以配置远程计算机以部署、测试和调试驱动程序。 配置远程计算机时，将安装 Windows 驱动程序测试框架运行时。

## <a name="installing-wdtf-runtime-library"></a>安装 WDTF 运行时库

### <a name="to-install-wdtf-runtime-library-using-visual-studio-and-the-wdk"></a>使用 Visual Studio 和 WDK 安装 WDTF 运行时库

1. 安装 Visual Studio，然后安装 WDK。

2. 配置远程计算机以进行测试和部署。 在 Visual Studio 中的 " **驱动程序** " 菜单上，指向 " **测试** "，然后选择 " **配置计算机 ...**"。

3. 配置测试计算机时，会安装 Windows 驱动程序测试框架运行时。

- 有关详细信息，请参阅：

  - [将驱动程序部署到测试计算机](../develop/deploying-a-driver-to-a-test-computer.md)

  - [预配计算机以便进行驱动程序部署和测试 (WDK 10)](../gettingstarted/provision-a-target-computer-wdk-8-1.md)  

### <a name="installing-the-wdtf-runtime-library-manually"></a>手动安装 WDTF 运行时库

安装 WDK 时，还会安装 Windows 驱动程序测试框架运行时的安装包。 需要将安装包复制到测试计算机并运行命令。 有关信息，请参阅在 [测试计算机上手动安装 WDTF 运行时库 () ](./wdtf-runtime-library.md#manually-installing-wdtf-on-a-test-computer-alternative-method) 在 [WDTF 运行时库](wdtf-runtime-library.md)中的替代方法。

## <a name="writing-tests-with-wdtf"></a>使用 WDTF 编写测试

WDK 提供用于通过 WDTF 编写测试的模板。 请参阅 [如何使用驱动程序测试模板编写驱动程序测试](../develop/how-to-write-a-driver-test-.md)。 你还可以使用模板为目标设备创建 WDTF 简单的 i/o 插件。 有关信息，请参阅为 [设备编写 WDTF 简单 i/o 插件](writing-a-wdtf-simpleio-plug-in-for-your-device.md)。

## <a name="running-wdtf-tests"></a>运行 WDTF 测试

使用 WDTF 驱动程序测试模板在 Visual Studio 中生成驱动程序测试时，新测试将可用于部署到测试计算机。 默认情况下，你创建的测试将显示在测试类别“我的测试类别”  中。 测试名称基于你选择的测试用例，其名称将类似于“我的即插即用意外删除测试”  。 在每次生成测试时，测试将被覆盖，并且可在 "轻松运行测试" 功能中运行。 有关详细信息，请参阅 [如何使用 Visual Studio 在运行时测试驱动程序](../develop/testing-a-driver-at-runtime.md)。