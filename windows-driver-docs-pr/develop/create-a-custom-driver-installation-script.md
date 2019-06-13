---
ms.assetid: 9F1E79FF-D38E-484A-8AEB-FC9A105BF709
title: 如何创建自定义的驱动程序安装脚本
description: 如果不只需要在测试计算机上安装驱动程序包，可以在安装时运行自定义的命令脚本。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34688d9e3b765f505c0fce0105b2c1d20449a7c5
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63382538"
---
# <a name="how-to-create-a-custom-driver-installation-script"></a>如何创建自定义的驱动程序安装脚本

如果部署方案不只需要在测试计算机上安装驱动程序包，可以选择在安装后运行自己的自定义命令脚本。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

-   已经过测试签名并准备好安装的驱动程序包。 必须先创建并生成驱动程序，然后再创建用于安装的驱动程序包。 有关详细信息，请参阅[生成驱动程序](building-a-driver.md)和[创建驱动程序包](creating-a-driver-package.md)。
-   测试针对部署配置和预配的计算机。 请参阅[如何在运行时使用 Visual Studio 测试驱动程序](testing-a-driver-at-runtime.md)。

<a name="instructions"></a>说明
------------

### <a name="span-idtorunyourowncustomcommandscriptsuponinstallationspanspan-idtorunyourowncustomcommandscriptsuponinstallationspanspan-idtorunyourowncustomcommandscriptsuponinstallationspanstep-1-to-run-your-own-custom-command-scripts-upon-installation"></a><span id="To_run_your_own_custom_command_scripts_upon_installation"></span><span id="to_run_your_own_custom_command_scripts_upon_installation"></span><span id="TO_RUN_YOUR_OWN_CUSTOM_COMMAND_SCRIPTS_UPON_INSTALLATION"></span>步骤 1：安装后运行你自己的自定义命令脚本

从驱动程序包的项目属性页，可以配置是否要在测试计算机上自动部署驱动程序包。 还可以从这些页运行自定义安装脚本。 可以选择在每次在每个配置中生成驱动程序解决方案时都自动部署驱动程序。 有关部署的详细信息，请参阅[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)和[驱动程序项目的部署属性](deployment-properties-for-driver-projects.md)。

1.  打开驱动程序包项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择“属性”  。

2.  在驱动程序包的属性页中，依次单击“配置属性”  、“驱动程序设置”  和“部署”  。

3.  单击“启用部署”  ，然后选择要使用的测试计算机。

4.  单击“自定义命令行”  。 在框中，键入要在安装后运行的自定义命令脚本。

5.  在“附加文件”  文本框中，添加要复制到测试计算机的命令脚本和其他安装文件。 部署驱动程序后，附加文件将复制到远程计算机上的 *%Systemdrive%* \\drivertest\\drivers 文件夹。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
* [驱动程序项目的部署属性](deployment-properties-for-driver-projects.md)
* [如何使用 Visual Studio 在运行时测试驱动程序](testing-a-driver-at-runtime.md)
* [生成驱动程序](building-a-driver.md)
* [创建驱动程序包](creating-a-driver-package.md)
 

 






