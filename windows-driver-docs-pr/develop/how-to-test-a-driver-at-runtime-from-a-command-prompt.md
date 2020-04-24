---
ms.assetid: 31CE7AE9-6444-4706-9C43-2B35038FA955
title: 如何在运行时通过命令提示符测试驱动程序
description: WDK 提供的设备测试组件使你能够在网络中的测试计算机上测试驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b913f148d2430c7068b16cb582d42dfe7e02708c
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "72839610"
---
# <a name="how-to-test-a-driver-at-runtime-from-a-command-prompt"></a>如何在运行时通过命令提示符测试驱动程序

WDK 提供的设备测试组件使你能够在网络中的测试计算机上测试驱动程序。 复制和安装必要文件之后，可以在 Visual Studio 之外使用这些组件。 可以使用这些组件来运行 Visual Studio 中提供的同一组设备驱动程序测试，以测试驱动程序的特性和功能。

从 WDK 8.1 起，可以使用命令脚本在测试计算机上复制和运行 HCK 测试套件。 请参阅[如何在 WDK 8.1 中运行 HCK 测试套件](run-the-hck-test-suites-in-the-wdk.md)。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

-   在用于开发的计算机上安装 Visual Studio 和 WDK。
-   在 Visual Studio 中，可以配置和预配测试计算机。 配置测试计算机时，WDK 驱动程序测试框架将自动启用测试计算机进行远程调试，并传输所需的测试二进制文件和支持文件。 按照[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1) 中的说明进行操作（如果尚未这样做）
-   虽然不推荐这样做，但你仍可以手动安装必要的测试组件。 请按照说明在测试计算机上安装[测试创作和执行框架 (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/index) 和 WDTF。 请参阅[在测试计算机上手动安装和卸载 TAEF](https://docs.microsoft.com/windows-hardware/drivers/taef/getting-started#manual_install_taef)和[在测试计算机上手动安装 WDTF](https://docs.microsoft.com/windows-hardware/drivers/ddi/index#manual_install_wdtf)。

<a name="instructions"></a>说明
------------

### <a name="span-idcopy_the_tests_to_the_test_computerspanspan-idcopy_the_tests_to_the_test_computerspanspan-idcopy_the_tests_to_the_test_computerspanstep-1-copy-the-tests-to-the-test-computer"></a><span id="Copy_the_tests_to_the_test_computer"></span><span id="copy_the_tests_to_the_test_computer"></span><span id="COPY_THE_TESTS_TO_THE_TEST_COMPUTER"></span>步骤 1：将测试复制到测试计算机上

-   从用于开发的计算机上复制[设备基础功能测试](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-fundamentals-tests)。 将文件夹 %ProgramFiles%\\Windows Kits\\8.0\\Testing\\Tests\\Device Fundamentals 复制到测试计算机。

### <a name="span-idrun_the_testsspanspan-idrun_the_testsspanspan-idrun_the_testsspanstep-2-run-the-tests"></a><span id="Run_the_tests"></span><span id="run_the_tests"></span><span id="RUN_THE_TESTS"></span>步骤 2：运行测试

运行测试的 TAEF 命令使用以下语法：

```cpp
Te.exe [/name:<Test Method>] [<Test Name>.dll | <Test Name.wsc> ]  [/rebootStateFile=<file> ] [/enablewttlogging]  [/P:"DQ= <>" ]  
```

<a name="remarks"></a>备注
-------

必须指定测试二进制文件 (.dll) 或脚本 (.wsc) 文件。 测试方法 ( **/name:** _&lt;test method&gt;_ ) 为可选。 有关测试名称和测试方法的信息，请参阅[设备基础功能测试](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-fundamentals-tests)。 有关指定测试参数的信息，请参阅[设备基础功能测试参数](how-to-select-and-configure-the-device-fundamental-tests.md)和 [Te.exe 命令选项](https://docs.microsoft.com/windows-hardware/drivers/taef/te-exe-command-line-parameters)。

例如，在具有特定设备 ID 的设备上运行 Devfund\_PnPDTest.dll 中的所有 PnP 测试。

```cpp
Te.exe  Devfund_PnPDTest.dll /P:"DQ=DeviceID='USB\ROOT_HUB\4&1CD5D022&0'"
```

例如，在具有特定设备 ID 的设备上运行 PnP 意外删除测试。

```cpp
Te.exe /name:"*PNPSurpriseRemoveAndRestartDevice" Devfund_PnPDTest.dll /P:"DQ=DeviceID='USB\ROOT_HUB\4&1CD5D022&0'"
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [设备基础功能测试](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-fundamentals-tests)
* [设备基础功能测试参数](how-to-select-and-configure-the-device-fundamental-tests.md)
* [如何在 WDK 8.1 中运行 HCK 测试套件](run-the-hck-test-suites-in-the-wdk.md)
* [测试创作和执行框架 (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/index)
* [Te.exe 命令选项](https://docs.microsoft.com/windows-hardware/drivers/taef/te-exe-command-line-parameters)
 

 






