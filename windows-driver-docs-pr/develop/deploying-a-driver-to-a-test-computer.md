---
ms.assetid: 328404BD-E888-4AAA-AA24-B57FD01E9E54
title: 将驱动程序部署到测试计算机
description: 在 Visual Studio 中，WDK 提供可让你在测试计算机上生成、部署和调试驱动程序的测试功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 613870a14b456ec66946a628f0ef1785a0202009
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370767"
---
# <a name="deploying-a-driver-to-a-test-computer"></a>将驱动程序部署到测试计算机

利用 Visual Studio 开发环境，WDK 提供可让你在测试计算机上生成、部署和调试驱动程序的测试功能。 基要使用 WDK 将驱动程序成功部署到测试系统，必须首先设置并配置测试计算机。 如果你想要在不同测试情境下测试驱动程序，你可以设置并配置多台计算机。

## <a name="span-idsetting_up_the_test_computerspanspan-idsetting_up_the_test_computerspanspan-idsetting_up_the_test_computerspansetting-up-the-test-computer"></a><span id="Setting_up_the_test_computer"></span><span id="setting_up_the_test_computer"></span><span id="SETTING_UP_THE_TEST_COMPUTER"></span>设置测试计算机


-   按照[预配计算机以便进行驱动程序部署和测试 (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1) 中的说明进行操作。

**注意**  如果你在设置测试计算机时遇到困难，请参阅[解决驱动程序部署、测试和调试的配置问题](troubleshooting-configuration-of-driver-deployment--testing-and-debugging.md)。

 

## <a name="span-idsetting_deployment_properties_for_your_driver_solutionspanspan-idsetting_deployment_properties_for_your_driver_solutionspanspan-idsetting_deployment_properties_for_your_driver_solutionspansetting-deployment-properties-for-your-driver-solution"></a><span id="Setting_deployment_properties_for_your_driver_solution"></span><span id="setting_deployment_properties_for_your_driver_solution"></span><span id="SETTING_DEPLOYMENT_PROPERTIES_FOR_YOUR_DRIVER_SOLUTION"></span>设置你的驱动程序解决方案的部署属性


从驱动程序项目的属性页，你可以对你希望如何针对测试部署驱动程序进行更多控制。 可以选择在每次在每个配置中生成驱动程序解决方案时都自动部署驱动程序。

1.  打开驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择“属性”  。
2.  在驱动程序项目的属性页中，依次单击“配置属性”  、“驱动程序安装”  和“部署”  。
3.  选择你已经配置的测试计算机，或选择你想要针对测试配置的计算机的名称。 请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

    在为你的驱动程序包项目启用部署时，该驱动程序将自动部署到你生成解决方案时选择的测试计算机。 你可以使用**部署**属性页配置驱动程序安装和部署的选项。 请参阅[驱动程序包项目的部署属性](deployment-properties-for-driver-projects.md)。

4.  当你在测试计算机上启用部署时，你还可以在测试计算机上自动启用并配置[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)、KMDF 验证程序或 UMDF 验证程序以增强测试的有效性。 若要为驱动程序包项目设置这些选项，请依次单击“配置属性”  、“驱动程序安装”  ，然后单击以下属性页。
    -   [驱动程序包项目的驱动程序验证程序属性](driver-verifier-properties-for--driver-projects.md)
    -   [驱动程序包项目的 KMDF 验证程序属性](kmdf-verifier-properties-for-driver-package-projects.md)
    -   [驱动程序包项目的 UMDF 验证程序属性](umdf-verifier-properties-for-driver-package-projects.md)

## <a name="span-idbuilding_a_driver_and_deploying_the_driver_to__test_computerspanspan-idbuilding_a_driver_and_deploying_the_driver_to__test_computerspanspan-idbuilding_a_driver_and_deploying_the_driver_to__test_computerspanbuilding-a-driver-and-deploying-the-driver-to-test-computer"></a><span id="Building_a_driver_and_deploying_the_driver_to__test_computer"></span><span id="building_a_driver_and_deploying_the_driver_to__test_computer"></span><span id="BUILDING_A_DRIVER_AND_DEPLOYING_THE_DRIVER_TO__TEST_COMPUTER"></span>生成驱动程序并将该驱动程序部署到测试计算机


1.  在部署驱动程序之前，请确保你可以生成驱动程序解决方案。 驱动程序解决方案必须包括驱动程序和驱动程序包，以便可以在测试计算机上安装驱动程序。 有关详细信息，请参阅[创建驱动程序包](creating-a-driver-package.md)和[生成驱动程序](building-a-driver.md)。
2.  在将驱动程序部署到测试计算机之前，你还需要为驱动程序包签名。 请参阅[在开发和测试期间为驱动程序签名](signing-a-driver-during-development-and-testing.md)。
3.  选择你已经配置的测试计算机。
4.  若要部署驱动程序，从“生成”  菜单中单击“生成解决方案”  或“部署解决方案”  ，或者按 **F5** 来进行生成、部署并开始调试。
5.  在测试计算机上，你可能会看到一个对话框，要求你确认应进行的更改。  在此情况下，在你确认之前，部署将暂停。

部署驱动程序时，驱动程序文件将复制到测试计算机上的 %Systemdrive%\\drivertest\\drivers 文件夹。 如果部署期间发生错误，你可以查看这些文件是否已复制到测试计算机。 请确认 .inf、.cat、测试证书和 .sys 文件以及其他任何必要的文件均位于 %systemdrive%\\drivertest\\drivers 文件夹下。

## <a name="span-idtroubleshooting_driver_deployment_spanspan-idtroubleshooting_driver_deployment_spanspan-idtroubleshooting_driver_deployment_spantroubleshooting-driver-deployment"></a><span id="Troubleshooting_driver_deployment_"></span><span id="troubleshooting_driver_deployment_"></span><span id="TROUBLESHOOTING_DRIVER_DEPLOYMENT_"></span>驱动程序部署疑难解答


下面是当你使用 Visual Studio 和 WDK 时将驱动程序部署到测试计算机的一些疑难解答提示。

**部署由于某个错误而失败，错误代码为 2**

添加以下注册表项：

**HKLM\Software\Microsoft\DriverTest\Service**

在此项下，创建 DWORD 值 **DebugSession**，并将其设置为 0。

此值只需要设置一次，它将保留供将来的部署使用。


<span id="Can_t_find_the_deployment_properties_for_the_driver_project"></span><span id="can_t_find_the_deployment_properties_for_the_driver_project"></span><span id="CAN_T_FIND_THE_DEPLOYMENT_PROPERTIES_FOR_THE_DRIVER_PROJECT"></span>**找不到驱动程序项目的部署属性**  
仅当你有驱动程序包时才会显示部署属性。 如果你的驱动程序解决方案没有驱动程序包项目，你需要添加一个。 驱动程序包包含组件，如安装所需的 INF 文件。 有关详细信息，请参阅[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)和[创建驱动程序包](creating-a-driver-package.md)。

添加了驱动程序包后，你可以在“解决方案资源管理器”中右键单击该驱动程序包项目，然后选择“属性”  。 在驱动程序包的属性页中，依次单击“配置属性”  、“驱动程序安装”  和“部署”  。

<span id="Problems_selecting__configuring_or_locating_the_target_computer"></span><span id="problems_selecting__configuring_or_locating_the_target_computer"></span><span id="PROBLEMS_SELECTING__CONFIGURING_OR_LOCATING_THE_TARGET_COMPUTER"></span>**选择、配置或查找目标计算机时遇到问题**  
有关如何使用 Windows 驱动程序工具包 (WDK) 8.1 和 Windows 驱动程序工具包 (WDK) 8 设置目标计算机的说明，请参阅[为驱动程序部署和测试预配计算机 (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。 如果你在预配目标计算机时遇到问题，请参阅[解决驱动程序部署、测试和调试的配置问题](troubleshooting-configuration-of-driver-deployment--testing-and-debugging.md)。

如果目标计算机运行的是 N 或 KN 版本的 Windows，则必须安装适用于 N 和 KN 版本的 Windows 的媒体功能包。 有关详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

<span id="Problems_installing_the_driver_on_64-bit_version_of_Windows"></span><span id="problems_installing_the_driver_on_64-bit_version_of_windows"></span><span id="PROBLEMS_INSTALLING_THE_DRIVER_ON_64-BIT_VERSION_OF_WINDOWS"></span>**在 64 位版本的 Windows 上安装驱动程序时遇到问题**  
从 Windows Vista 起，所有 64 位版本的 Windows 均需要驱动程序代码以获得加载驱动程序所需的数字签名。 请参阅[为驱动程序签名](signing-a-driver.md)和[在开发和测试期间为驱动程序签名](signing-a-driver-during-development-and-testing.md)。

<span id="Problems_installing_the_driver__general_"></span><span id="problems_installing_the_driver__general_"></span><span id="PROBLEMS_INSTALLING_THE_DRIVER__GENERAL_"></span>**安装驱动程序时遇到问题（常规）**  
WDK 可以在测试计算机上部署并安装驱动程序包，但前提是驱动程序有安装所需的所有必要的组件，如 INF 文件。 有关详细信息，请参阅[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)。 请确保你可以在 Visual Studio 和 WDK 之外安装驱动程序。 例如，使用设备控制台实用工具 [Devcon](https://docs.microsoft.com/windows-hardware/drivers/devtest/devcon) 测试是否可以安装驱动程序。 请确保将设备（如果有）连接到目标计算机。 有关详细信息，请参阅[设备和驱动程序安装](https://docs.microsoft.com/windows-hardware/drivers/install/index)和[创建驱动程序包](creating-a-driver-package.md)。
