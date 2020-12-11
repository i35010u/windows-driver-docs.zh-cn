---
title: 如何测试驱动程序包
description: 可以使用 Visual Studio 在测试计算机上部署和安装驱动程序包，然后验证该驱动程序是否已安装并运行。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c54fb54551369a8cbc1271cd89cc235b6f2720d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784115"
---
# <a name="how-to-test-a-driver-package"></a>如何测试驱动程序包

可以使用 Visual Studio 在测试计算机上部署和安装驱动程序包，然后验证该驱动程序是否已安装并运行。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

-   准备好安装的驱动程序包。 必须先创建并生成驱动程序，然后再创建用于安装的驱动程序包。 有关详细信息，请参阅[生成驱动程序](building-a-driver.md)和[创建驱动程序包](creating-a-driver-package.md)。
-   如果尚未完成此操作，请按照[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md) 中的说明进行操作。
-   配置并预配测试计算机后，可以使用 Visual Studio 在测试计算机上部署驱动程序、安排测试、调试驱动程序。 有关部署以及如何在生成时自动部署驱动程序的信息，请参阅[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)。

<a name="instructions"></a>说明
------------

### <a name="span-idto_test_the_driver_installation_on_a_test_computerspanspan-idto_test_the_driver_installation_on_a_test_computerspanspan-idto_test_the_driver_installation_on_a_test_computerspanstep-1-to-test-the-driver-installation-on-a-test-computer"></a><span id="To_test_the_driver_installation_on_a_test_computer"></span><span id="to_test_the_driver_installation_on_a_test_computer"></span><span id="TO_TEST_THE_DRIVER_INSTALLATION_ON_A_TEST_COMPUTER"></span>步骤 1：测试驱动程序在测试计算机上的安装

在配置和预配测试计算机后，可以配置驱动程序包项目，以让它自动部署和安装到测试计算机上。

1.  打开驱动程序项目的属性页。 在“解决方案资源管理器”中，选择并按住（或右键单击）驱动程序项目，然后选择“属性”。
2.  在驱动程序的属性页中，依次选择“配置属性”、“驱动程序安装”、“部署”  。
3.  选择“启用部署”  选项。 有关详细信息，请参阅[驱动程序项目的部署属性](deployment-properties-for-driver-projects.md)。
4.  选择已配置为 **远程计算机** 的测试计算机。
5.  在“驱动程序安装选项”下，选择“安装并验证”，然后选择“默认驱动程序安装任务”。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
* [测试驱动程序](testing-a-driver.md)
 

