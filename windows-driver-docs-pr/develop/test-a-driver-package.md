---
ms.assetid: 5BA0A193-1147-4BAD-A6CA-453856E621A2
title: 如何测试驱动程序包
description: 可以使用 Visual Studio 在测试计算机上部署和安装驱动程序包，然后验证该驱动程序是否已安装并运行。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59f8edbabc28832d2e589d2eed4d173ea0ca5669
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364213"
---
# <a name="how-to-test-a-driver-package"></a>如何测试驱动程序包

可以使用 Visual Studio 在测试计算机上部署和安装驱动程序包，然后验证该驱动程序是否已安装并运行。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

-   准备好安装的驱动程序包。 必须先创建并生成驱动程序，然后再创建用于安装的驱动程序包。 有关详细信息，请参阅[生成驱动程序](building-a-driver.md)和[创建驱动程序包](creating-a-driver-package.md)。
-   如果尚未完成此操作，请按照[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1) 中的说明进行操作。
-   配置并预配测试计算机后，可以使用 Visual Studio 在测试计算机上部署驱动程序、安排测试、调试驱动程序。 有关部署以及如何在生成时自动部署驱动程序的信息，请参阅[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)。

<a name="instructions"></a>说明
------------

### <a name="span-idto_test_the_driver_installation_on_a_test_computerspanspan-idto_test_the_driver_installation_on_a_test_computerspanspan-idto_test_the_driver_installation_on_a_test_computerspanstep-1-to-test-the-driver-installation-on-a-test-computer"></a><span id="To_test_the_driver_installation_on_a_test_computer"></span><span id="to_test_the_driver_installation_on_a_test_computer"></span><span id="TO_TEST_THE_DRIVER_INSTALLATION_ON_A_TEST_COMPUTER"></span>步骤 1：测试驱动程序在测试计算机上的安装

在配置和预配测试计算机后，可以配置驱动程序包项目，以让它自动部署和安装到测试计算机上。

1.  打开驱动程序项目的属性页。 在“解决方案资源管理器”中右键单击驱动程序项目，并选择“属性”  。
2.  在驱动程序的属性页中，依次单击“配置属性”  、“驱动程序安装”  和“部署”  。
3.  选择“启用部署”  选项。 有关详细信息，请参阅[驱动程序项目的部署属性](deployment-properties-for-driver-projects.md)。
4.  选择已配置为**远程计算机**的测试计算机。
5.  在“驱动程序安装选项”  下，单击“安装并验证”  ，然后选择“默认驱动程序安装任务”  。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
* [测试驱动程序](testing-a-driver.md)
 

 






