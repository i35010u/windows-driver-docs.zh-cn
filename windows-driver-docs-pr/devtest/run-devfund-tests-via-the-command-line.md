---
title: 如何通过命令行运行 DevFund 测试
description: WDK 提供的测试二进制文件和工具支持轻松地从命令行运行设备基础功能测试。
keywords:
- 说明测试
- 命令行
ms.date: 06/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: de9a0d34ca201833aacb5857a3260f6f9e71bf4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340234"
---
# <a name="how-to-run-the-devfund-tests-via-the-command-line"></a>如何通过命令行运行 DevFund 测试

**概述**

有几种方法来通过命令行运行说明和 SysFund 测试。  此页上的说明适用于通过命令行使用 Visual Studio 和 Windows Driver Kit (WDK)，但如果不设置通过 Visual Studio 的测试系统运行测试。

运行说明和 SysFund 测试的其他方法包括：

- 硬件 Lab Kit (HLK):可以从命令行运行测试[HLK 客户端测试计算机](https://docs.microsoft.com/windows-hardware/test/hlk/testref/reproduce-the-test-failure-by-running-the-test-from-the-command-line)

- 测试"预配"通过 Visual Studio 的计算机：[通过命令行运行测试](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-test-a-driver-at-runtime-from-a-command-prompt)

- 企业 Windows 驱动程序工具包 （EWDK-不需要 Visual Studio）：如果未安装 Visual Studio，并且将不使用[EWDK 用于命令行上运行测试](https://docs.microsoft.com/windows-hardware/drivers/devtest/configure-the-machine-for-testing)

**设置**


请注意因为 WDTF 安装在系统上安装的驱动程序必须从提升/管理员命令提示符执行以下命令。 下面的说明假定系统体系结构是 x64。 以下步骤可能需要调整为其他体系结构。

**步骤 1** :[安装 Visual Studio 和 Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

**步骤 2** :测试使用[TAEF](https://docs.microsoft.com/windows-hardware/drivers/taef/)服务。  

若要安装 TAEF 服务 (Te.service)，请转到```%PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\TAEF\x64```并运行以下命令以获取服务已启动：

1. ```wex.services.exe /install:te.service``` （验证已成功安装 te.service）

2. ```sc start te.service``` (验证状态是启动\_PENDING)

3. ```sc query te.service``` (验证状态为正在运行)

4. ```sc qc te.service``` (确认启动\_类型是自动\_启动)

将此目录添加到系统 PATH 环境变量并重新启动提升的命令提示符。

**步骤 3** :安装[WDTF](https://docs.microsoft.com/windows-hardware/drivers/wdtf/)通过导航到 WDTF MSI 的位置 (```%PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\```) 和安装所需的体系结构的包。 指定的位置和安装日志文件的名称 **%USERPROFILE%\Desktop\WDTFInstall.log**在此示例中：

 
``` 
cd %PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\
```

```
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64\_en-us.msi" /l\* "%USERPROFILE%\Desktop\WDTFInstall.log"
```

WDTF MSI 安装到 WDTF **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\WDTF**由于此示例使用 64 位 WDTF MSI，即使 WDTF MSI 是下 **%programfiles （x86） %**


**步骤 4** :配置用于测试的计算机：

- 配置计算机以收集完全转储或附加内核调试程序。

- 因为测试可能可以重新启动计算机并需要控制睡眠周期，永远不会进入睡眠状态，永远不会关闭显示和自动登录到测试帐户 (netplwiz.exe) 将计算机配置。 请注意应谨慎使用该自动登录。

**步骤 5** :运行测试。  说明测试位于 **%programfiles (X86) %\Windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund**。

用于运行说明测试的基本命令是窗体：

```
Te.exe Devfund_<testname>.dll /name:"<test case name>" /p:"DQ=DeviceID='<Device Instance Path of device under test from Device Manager>'" /RebootStateFile:state.xml
```

其中&lt;_测试用例名称_&gt;测试二进制文件中的测试的名称。

/**名称**开关是可选的。 由于某些测试二进制文件包含多个测试 /**名称**开关指定应运行哪些测试。 如果未指定，将按顺序执行测试二进制文件中包含的所有测试。 可以通过运行以下命令获得的测试二进制文件中的测试列表：

```
Te.exe Devfund\<testname>.dll /list
```

例如，说明\_PnPDTest.dll 包含大部分 PnP 相关测试：

```
Te.exe Devfund_PnPDTest_WLK_Functional.dll /list

Test Authoring and Execution Framework v10.21 for x64

    Devfund_PnPDTest_WLK_Functional.dll

        PNPDTest

            PNPDTest::PNPDisableAndEnableDevice

            PNPDTest::PNPRemoveAndRestartDevice

            PNPDTest::PNPCancelRemoveDevice

            PNPDTest::PNPCancelStopDevice

            PNPDTest::PNPTryStopAndRestartDevice

            PNPDTest::PNPTryStopDeviceRequestNewResourcesAndRestartDevice

            PNPDTest::PNPTryStopDeviceAndFailRestart

            PNPDTest::PNPSurpriseRemoveAndRestartDevice

            PNPDTest::PNPDIFRemoveAndRescanParentDevice

            PNPDTest::DisableEnhancedDeviceTestingSupport
```


要运行此测试二进制文件从单个测试的命令可能如下所示：

```
c:\temp\Te.exe Devfund_PnPDTest_WLK_Functional.dll /name:PNPDTest::PNPSurpriseRemoveAndRestartDevice* /p:"DQ=DeviceID='my\device\id'" /RebootStateFile:state.xml
```
