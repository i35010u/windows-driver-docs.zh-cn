---
title: 如何通过命令行运行 DevFund 测试
description: WDK 提供的测试二进制文件和工具支持轻松地从命令行运行设备基础功能测试。
keywords:
- DevFund 测试
- 命令行
ms.date: 06/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: e5fca7e3683f8664779a1827544db9fda31dd697
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382095"
---
# <a name="how-to-run-the-devfund-tests-via-the-command-line"></a>如何通过命令行运行 DevFund 测试

**概述**

通过命令行运行 DevFund 和 SysFund 测试有多种方法。  此页上的说明用于通过命令行运行测试和 Visual Studio，Windows 驱动程序工具包 (WDK) ，但不通过 Visual Studio 预配测试系统。

运行 DevFund 和 SysFund 测试的其他方法包括：

- 硬件实验室工具包 (的 HLK) ：可在[hlk 客户端测试计算机](/windows-hardware/test/hlk/testref/reproduce-the-test-failure-by-running-the-test-from-the-command-line)上从命令行运行测试

- 通过 Visual Studio 进行测试计算机 "预配"： [通过命令行运行测试](../develop/how-to-test-a-driver-at-runtime-from-a-command-prompt.md)

- 企业 Windows 驱动程序工具包 (EWDK-不需要 Visual Studio) ：如果未安装 Visual Studio 且不会使用它，请 [使用 EWDK 在命令行上运行测试](./configure-the-machine-for-testing.md)

**安装**


请注意，必须在提升的/管理员命令提示符下执行以下命令，因为 WDTF 安装会在系统上安装驱动程序。 以下说明假定系统体系结构为 x64。 对于其他体系结构，可能需要调整以下步骤。

**步骤 1** ： [安装 Visual Studio 和 Windows 驱动程序工具包 (WDK) ](../download-the-wdk.md)

**步骤 2** ：测试使用 [TAEF](../taef/index.md) 服务。  

若要将 TAEF 服务安装 (Te) ，请转到 ```%PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\TAEF\x64``` ，并运行以下命令以启动该服务：

1. ```wex.services.exe /install:te.service``` (验证 te 是否成功安装了服务) 

2. ```sc start te.service``` (验证 "状态" 是否为 "启动 \_ 挂起" ) 

3. ```sc query te.service``` (验证 "状态" 是否为 "正在运行" ) 

4. ```sc qc te.service``` (验证 "启动 \_ 类型" 是否为 "自动 \_ 启动" ) 

将此目录添加到系统路径环境变量，然后重新启动提升的命令提示符。

**步骤 3** ：通过[WDTF](../wdtf/index.md)导航到 WDTF MSI (的位置 ```%PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\```) 并为所需的体系结构安装包来安装 WDTF。 指定安装日志文件的位置和名称，在此示例中为 **%USERPROFILE%\Desktop\WDTFInstall.log** ：

 
``` 
cd %PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\
```

```
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64\_en-us.msi" /l\* "%USERPROFILE%\Desktop\WDTFInstall.log"
```

WDTF MSI 将 WDTF 安装到 **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\WDTF** ，因为此示例使用的是64位 WDTF msi，即使 WDTF msi 低于 **% PROGRAMFILES (X86) %**


**步骤 4** ：配置计算机以进行测试：

- 将计算机配置为收集完全转储或附加内核调试器。

- 由于这些测试可能会重新启动计算机并需要控制睡眠周期，因此请将计算机配置为从不睡眠、从不关闭显示，并自动登录到测试帐户 ( # A0) 。 请注意，应谨慎使用自动登录。

**步骤 5** ：运行测试。  DevFund 测试位于 **X86) % \ Windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund 的% PROGRAMFILES (**。

用于运行 DevFund 测试的基本命令的格式为：

```
Te.exe Devfund_<testname>.dll /name:"<test case name>" /p:"DQ=DeviceID='<Device Instance Path of device under test from Device Manager>'" /RebootStateFile:state.xml
```

其中， &lt; _测试用例名称_ &gt; 是测试二进制文件中测试的名称。

/ **Name** 开关是可选的。 由于某些测试二进制文件包含多个测试，因此/ **name** 开关指定应运行的测试。 如果未指定，则按顺序执行测试二进制文件中包含的所有测试。 可以通过运行以下命令来获取测试二进制文件中的测试列表：

```
Te.exe Devfund\<testname>.dll /list
```

例如，Devfund \_PnPDTest.dll 包含大多数与 PnP 相关的测试：

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


用于从此测试二进制文件运行单个测试的命令可能如下所示：

```
c:\temp\Te.exe Devfund_PnPDTest_WLK_Functional.dll /name:PNPDTest::PNPSurpriseRemoveAndRestartDevice* /p:"DQ=DeviceID='my\device\id'" /RebootStateFile:state.xml
```