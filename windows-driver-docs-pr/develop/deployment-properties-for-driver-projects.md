---
ms.assetid: 7193DA4B-2461-4E00-90B4-C31B93C8E9BD
title: 驱动程序包项目的部署属性
description: 你可以在项目的每个配置中配置远程测试计算机上驱动程序包的自动部署。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4790fa57c877d9b74a2bd46fc80cef87528a20a5
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63356633"
---
# <a name="deployment-properties-for-driver-package-projects"></a>驱动程序包项目的部署属性

你可以在项目的每个配置中配置远程测试计算机上驱动程序包的自动部署。 从驱动程序的项目属性页，你可以对你希望针对测试部署驱动程序的方式进行更多控制。 你可以选择在每次在每个配置中生成驱动程序解决方案时都自动部署驱动程序。 有关部署的详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909) 和[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)。

## <a name="span-idsettingdeploymentpropertiesfordriverpackageprojectsspanspan-idsettingdeploymentpropertiesfordriverpackageprojectsspanspan-idsettingdeploymentpropertiesfordriverpackageprojectsspansetting-deployment-properties-for-driver-package-projects"></a><span id="Setting_deployment_properties_for_driver_package_projects"></span><span id="setting_deployment_properties_for_driver_package_projects"></span><span id="SETTING_DEPLOYMENT_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>设置驱动程序包项目的部署属性


1.  打开驱动程序包的属性页。 在“解决方案资源管理器”中，右键单击驱动程序包项目，并选择“属性”  。

    **注意**  如果你的驱动程序解决方案没有驱动程序包项目，你需要添加一个。 请参阅[创建驱动程序包](creating-a-driver-package.md)。 仅当你有驱动程序包时才会显示部署属性。
2.  在驱动程序包的属性页中，依次单击“配置属性”  、“驱动程序安装”  和“部署”  。
3.  选择“启用部署”  选项。 选中此选项后，你可以选择要使用的测试计算机，并且可以配置驱动程序安装和部署的选项。

## <a name="span-idprojectconfigurationandplatformspanspan-idprojectconfigurationandplatformspanspan-idprojectconfigurationandplatformspanproject-configuration-and-platform"></a><span id="Project_Configuration_and_Platform"></span><span id="project_configuration_and_platform"></span><span id="PROJECT_CONFIGURATION_AND_PLATFORM"></span>项目配置和平台


配置列表和平台列表可让你为不同项目配置和平台组合应用不同的部署设置。 例如，你可以使用一组调试版本的部署选项将驱动程序部署到一台测试计算机，使用发布版本的部署选项将驱动程序部署到另一台测试计算机。

## <a name="span-idenablingdeploymentspanspan-idenablingdeploymentspanspan-idenablingdeploymentspanenabling-deployment"></a><span id="Enabling_deployment"></span><span id="enabling_deployment"></span><span id="ENABLING_DEPLOYMENT"></span>启用部署


你可以通过选择“启用部署”  来选择在测试计算机上部署驱动程序包。 结合配置列表，你可以选择为调试版本禁用部署并为发布版本启用部署。

若要确保测试的是最新版本的驱动程序，请选择“部署前删除以前的驱动程序版本”  。

## <a name="span-idtargetcomputernamespanspan-idtargetcomputernamespanspan-idtargetcomputernamespantarget-computer-name"></a><span id="Target_computer_name"></span><span id="target_computer_name"></span><span id="TARGET_COMPUTER_NAME"></span>目标计算机名称


你可以选择要用于部署和测试的目标计算机。 如果你已经配置了测试计算机，则可以从此列表中选择。 如果你尚未配置测试计算机，则可以使用“浏览”  按钮配置一个。 有关配置测试计算机的详细信息，请参阅[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)。 请确保项目配置和平台与测试系统的目标体系结构匹配。 尝试在运行 x64 版本 Windows 的系统上安装 x86 (Win32) 驱动程序时发生常见部署错误。 在配置测试计算机时，也可以运行内核模式调试程序。 有关详细信息，请参阅[在 Visual Studio 中设置内核模式调试](https://msdn.microsoft.com/windows/hardware/hh439376)。

## <a name="span-iddriverinstallationoptionsspanspan-iddriverinstallationoptionsspanspan-iddriverinstallationoptionsspandriver-installation-options"></a><span id="Driver_installation_options"></span><span id="driver_installation_options"></span><span id="DRIVER_INSTALLATION_OPTIONS"></span>驱动程序安装选项


**不安装 -** 这是默认选项。 如果你要将驱动程序包导入[驱动程序存储](https://msdn.microsoft.com/Library/Windows/Hardware/Ff544868)或者如果你要在测试计算机上启用和设置驱动程序验证程序选项，则可以选择不安装。

**硬件 ID 驱动程序更新 -** 若要为实际的硬件设备部署驱动程序，请改用“安装并验证”  。 若要部署驱动程序作为根枚举驱动程序，可以使用**硬件 ID 驱动程序更新**或**安装并验证**。 如果你选择使用“硬件 ID 驱动程序更新”，必须输入出现在 INF 文件中的同一个硬件 ID，并且该硬件 ID 的格式必须为“Root\\Xxx”。 如果选择此选项，文件将复制到远程计算机上的 %*Systemdrive*%\\drivertest\\drivers 文件夹。 设备控制台实用工具 [Devcon](https://msdn.microsoft.com/Library/Windows/Hardware/Ff544707) 从程序包安装该硬件 ID 和 INF 文件的驱动程序。 例如，你可以选择“硬件 ID 驱动程序更新”  并将 HWID 设置为 **Root\\** <em>yourprojectname</em>。 请确保项目名称不包含任何空格。

**自定义命令行 -** 你可以选择在安装后运行自己的自定义命令脚本。 如果你想要运行自定义命令脚本，请确保在“附加文件”  部分下添加必要文件。 附加文件将复制到远程计算机上的 *%Systemdrive%* \\drivertest\\drivers 文件夹。

**安装并验证 -** 你可以选择使用自动测试脚本对安装进行测试。 如果你选择此选项，并指定“默认驱动程序包安装任务(可能重新启动)”  或“默认打印机驱动程序包安装任务(可能重新启动)”  ，则测试将读取驱动程序的 INF 文件并安装驱动程序。 然后，测试将验证该驱动程序是否已启动且正在运行。 完成后，测试将提供有关安装任务成功与否的详细信息。

**可选设备查询 -** 默认值为“%PathToInf%”  。 将自动替换驱动程序的 INF 文件的路径。 应该无需更改此值，除非你需要将 INF 文件放到其他位置。

## <a name="span-idadditionalfilesspanspan-idadditionalfilesspanspan-idadditionalfilesspanadditional-files"></a><span id="Additional_Files"></span><span id="additional_files"></span><span id="ADDITIONAL_FILES"></span>附加文件


你可以使用“附加文件”  框来指定想要复制到远程测试计算机的自定义安装脚本或应用程序。 你在此处指定的文件将添加到远程计算机上的 *%Systemdrive%* \\drivertest\\drivers 文件夹。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
* [如何使用 Visual Studio 在运行时测试驱动程序](testing-a-driver-at-runtime.md)
* [在 Visual Studio 中设置内核模式调试](https://msdn.microsoft.com/windows/hardware/hh439376)
 

 






