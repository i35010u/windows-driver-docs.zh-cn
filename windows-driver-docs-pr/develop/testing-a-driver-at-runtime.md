---
title: 如何使用 Visual Studio 在运行时测试驱动程序
description: 你可以在 Visual Studio 中使用 WDK 扩展，在网络中的测试计算机上方便地生成、部署、安装和测试驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3359cf286ed29e02377db16ae3772c10872f79f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784113"
---
# <a name="how-to-test-a-driver-at-runtime-using-visual-studio"></a>如何使用 Visual Studio 在运行时测试驱动程序

Visual Studio 的 WDK 扩展提供设备测试接口，可让你在网络中的测试计算机上方便地生成、部署、安装和测试驱动程序。 WDK 提供一系列设备驱动程序测试，你可以用来测试驱动程序的特性和功能。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

-   就绪可安装的驱动程序包。 必须先创建并生成驱动程序，然后再创建用于安装的驱动程序包。 有关详细信息，请参阅[生成驱动程序](building-a-driver.md)和[创建驱动程序包](creating-a-driver-package.md)。
-   驱动程序必须经过测试签名。 有关详细信息，请参阅[为驱动程序签名](signing-a-driver.md)。
-   一台测试计算机（或多台）。 测试计算机必须与你用于开发的计算机位于同一个网络。 这两台计算机必须连接到同一个域，或者都在同一工作组下连接到网络。 测试计算机应该运行你想要定位测试目标的 Windows 版本。 
-   要测试的设备。
-   （*建议*）设置与测试计算机的内核模式调试连接。 若要使用用于内核模式调试的网络连接，目标计算机必须运行 Windows 8。 在运行 Windows 7 或 Windows Vista 的计算机上，你可以设置 USB、1394 或串行连接以用于内核模式调试。 有关详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md)。

<a name="instructions"></a>说明
------------

### <a name="span-idconfigure_computers_for_testingspanspan-idconfigure_computers_for_testingspanspan-idconfigure_computers_for_testingspanstep-1-configure-computers-for-testing"></a><span id="Configure_computers_for_testing"></span><span id="configure_computers_for_testing"></span><span id="CONFIGURE_COMPUTERS_FOR_TESTING"></span>步骤 1：配置计算机以进行测试

在 Visual Studio 中，可以配置和预配测试计算机。 配置测试计算机时，WDK 驱动程序测试框架将自动启用测试计算机进行远程调试，并传输测试二进制文件和支持文件。

1.  如果尚未完成此操作，请按照[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md) 中的说明进行操作。
2.  将你想要测试的设备连接到测试计算机。

配置并预配测试计算机后，可以使用 Visual Studio 在测试计算机上部署驱动程序、安排测试、调试驱动程序。 有关部署以及如何在生成时自动部署驱动程序的信息，请参阅[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)。

你还可以启用并设置[驱动程序验证程序](../devtest/driver-verifier.md)（驱动程序的运行时验证工具）的选项。 当你在测试计算机上运行测试时，驱动程序验证程序会监视你的驱动程序。 有关针对部署设置驱动程序验证程序选项的信息，请参阅[驱动程序项目的驱动程序验证程序属性](driver-verifier-properties-for--driver-projects.md)。

你也可以在 Visual Studio 外部运行测试，有关详细信息，请参阅[如何在运行时从命令提示符测试驱动程序](how-to-test-a-driver-at-runtime-from-a-command-prompt.md)。 从 WDK 8.1 起，可以使用命令脚本在测试计算机上复制和运行 HCK 测试套件。 请参阅[如何在 WDK 8.1 中运行 HCK 测试套件](run-the-hck-test-suites-in-the-wdk.md)。

### <a name="span-idselect_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__81_spanspan-idselect_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__81_spanspan-idselect_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__81_spanstep-2-select-an-hck-test-suite-to-run-on-the-test-computer-using-wdk-81"></a><span id="Select_an_HCK_Test_Suite_to_run_on_the_test_computer__using_WDK__8.1_"></span><span id="select_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__8.1_"></span><span id="SELECT_AN_HCK_TEST_SUITE_TO_RUN_ON_THE_TEST_COMPUTER__USING_WDK__8.1_"></span>步骤 2：选择要在测试计算机上运行的 HCK 测试套件（使用 WDK 8.1）

从 WDK 8.1 开始，你可以选择要在测试计算机上运行的 HCK 测试套件。 HCK 测试套件包括[设备基础功能测试](../devtest/device-fundamentals-tests.md)，以及图形、映像、无线 LAN、移动宽带（CDMA 和 GSM）和 WiFi Direct 设备的 Windows 硬件认证工具包 (HCK) 基本测试。

-   请参阅[如何在 WDK 8.1 中运行 HCK 测试套件](run-the-hck-test-suites-in-the-wdk.md)。

### <a name="span-idselect_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_81_spanspan-idselect_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_81_spanspan-idselect_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_81_spanstep-3-select-the-tests-to-run-on-the-test-computer-wdk-8-and-wdk-81"></a><span id="Select_the_tests_to_run_on_the_test_computer__WDK_8_and_WDK_8.1_"></span><span id="select_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_8.1_"></span><span id="SELECT_THE_TESTS_TO_RUN_ON_THE_TEST_COMPUTER__WDK_8_AND_WDK_8.1_"></span>步骤 3：选择要在测试计算机上运行的测试（WDK 8 和 WDK 8.1）

若要使不同测试目标上的驱动程序测试更加容易，应将测试安排为针对称为“测试组”  的单元中的测试系统运行。 驱动程序测试组是你选择要在测试计算机上运行的测试的集合。 驱动程序测试组帮助你整理每个测试轮次的测试和测试结果。 可以将测试结果保存到单独的文件夹中。 你可以创建和管理测试组，更改传递到测试组中的测试的参数，并安排这些测试针对测试系统运行。

1.  从“驱动程序”菜单中，选择“测试”，然后选择“测试组资源管理器”。
2.  在“驱动程序测试组资源管理器”窗口中，选择“创建新测试组”按钮。 或者，在“驱动程序”菜单中选择“新建测试组”。
3.  在你创建的组的“驱动程序测试组”  窗口中，在“测试组名称”  文本框内键入一个用来识别该组的名称。 默认名称是 Driver Test Group\_*nnnnn*，其中 *nnnnn* 表示测试组的编号
4.  选择“添加/删除测试”。
5.  在“添加或删除驱动程序测试”  对话框中，你可以指定驱动程序测试类别和体系结构（所有、x86、x64、ARM）。 默认情况下会显示所有测试。 若要查看测试类别，选择“驱动程序测试类别”下拉列表中的文件夹。

    例如，在 WDK 8 中，若要选择 [Windows 硬件认证工具包 (HCK)](/windows-hardware/test/hlk/) 中使用的所有设备基础知识测试，选择“所有测试”、“认证”和“设备基础知识”。 有关测试的信息，请参阅[如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)。

    在 WDK 8.1 中，设备基础功能测试位于“所有测试”  、“HCK 测试”  、“认证”  和“设备基础”  文件夹下。 在 WDK 8.1 中，驱动程序测试类别包括 HCK（基本）测试。 请参阅[如何在 WDK 8.1 中运行 HCK 测试套件](run-the-hck-test-suites-in-the-wdk.md)了解详细信息。

6.  请确保选择与目标测试计算机体系结构（x86、x64、ARM）匹配的测试。 使用 **体系结构筛选器** 来仅显示将在测试计算机上运行的那些测试。
7.  选择 &gt;&gt; 添加已选择的测试。

### <a name="span-idconfigure_test_parametersspanspan-idconfigure_test_parametersspanspan-idconfigure_test_parametersspanstep-4-configure-test-parameters"></a><span id="Configure_test_parameters"></span><span id="configure_test_parameters"></span><span id="CONFIGURE_TEST_PARAMETERS"></span>步骤 4：配置测试参数

在为测试组选择测试后，你可以配置传递到驱动程序测试的任何一个运行时参数。 例如，许多设备基础功能测试具有参数 *DQ*，它代表“设备查询”。 这是[简单数据评估语言](../wdtf/simple-data-evaluation-language-overview.md) (SDEL) 查询。 [Windows 驱动程序测试框架](../wdtf/index.md)提供了 SDEL 作为查询语言，以简化根据属性或关系收集目标的任务。

例如，若要只为 USB 设备运行测试，请使用设备查询：class='usb'。 你可以更改测试组中每个测试参数的值。

1.  你可以选择“驱动程序测试组”窗口中测试的名称，查看和编辑测试的所有运行时测试参数。 “驱动程序测试组”  窗口提供对所选测试的说明，并且还提供对你选择的测试参数的说明。 有关设置测试参数的信息，请参阅[如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)
2.  选择测试后，设置参数，并为组命名，然后选择“保存”。

    保存测试组时，测试组将变为当前选择的测试组，测试组的名称将显示在“驱动程序测试”工具栏中。 你现在可以针对当前选择的远程测试计算机（同时显示在“驱动程序测试”工具栏中）运行测试。

### <a name="span-idbuild_and_deploy_the_driverspanspan-idbuild_and_deploy_the_driverspanspan-idbuild_and_deploy_the_driverspanstep-5-build-and-deploy-the-driver"></a><span id="Build_and_deploy_the_driver"></span><span id="build_and_deploy_the_driver"></span><span id="BUILD_AND_DEPLOY_THE_DRIVER"></span>步骤 5：生成和部署驱动程序

-   从“生成”菜单中选择“部署选择方案” 。

有关在生成时自动部署驱动程序的信息，请参阅[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)。 有关在测试计算机上自动设置驱动程序验证程序选项的信息，请参阅[驱动程序项目的驱动程序验证程序属性](driver-verifier-properties-for--driver-projects.md)。 你应始终在测试计算机上启用驱动程序验证程序。

### <a name="span-idrun_the_tests_on_the_test_computerspanspan-idrun_the_tests_on_the_test_computerspanspan-idrun_the_tests_on_the_test_computerspanstep-6-run-the-tests-on-the-test-computer"></a><span id="Run_the_tests_on_the_test_computer"></span><span id="run_the_tests_on_the_test_computer"></span><span id="RUN_THE_TESTS_ON_THE_TEST_COMPUTER"></span>步骤 6：在测试计算机上运行测试

-   从“驱动程序”菜单中，选择“测试”&gt;“运行测试” 。 默认情况下，“运行”测试命令将运行当前所选测试组中的所有测试。

<a name="remarks"></a>备注
-------

有关驱动程序测试和测试类别的信息，请参阅[如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)。 有关测试框架的信息，请参阅[测试授权和执行框架](../taef/index.md) (TAEF) 和 [Windows 驱动程序测试框架](../wdtf/index.md) (WDTF)。

你可以编写自己的驱动程序测试，并在测试计算机上部署这些测试。 有关详细信息，请参阅[如何编写驱动程序测试](how-to-write-a-driver-test-.md)。

在开发周期的早期在 Visual Studio 中运行设备基础功能测试，这将有助于你最终准备好使用 [Windows 硬件认证工具包 (HCK)](/windows-hardware/test/hlk/) 测试驱动程序。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [如何在 WDK 8.1 中运行 HCK 测试套件](run-the-hck-test-suites-in-the-wdk.md)
* [如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
* [Windows 调试入门](../debugger/getting-started-with-windows-debugging.md)
* [硬件认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))
* [Windows 硬件认证工具包 (HCK)](/windows-hardware/test/hlk/)
* [如何在运行时通过命令提示符测试驱动程序](how-to-test-a-driver-at-runtime-from-a-command-prompt.md)
