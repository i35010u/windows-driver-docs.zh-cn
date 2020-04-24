---
ms.assetid: eaefc81a-b5e3-4763-bf51-8ec47f620e72
title: 创建驱动程序包
description: 创建驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a778114e57284cba6a460c4a257e766fa4d76d37
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67370809"
---
# <a name="creating-a-driver-package"></a>创建驱动程序包

## <a name="span-iddriver_projects_and_packagesspanspan-iddriver_projects_and_packagesspanspan-iddriver_projects_and_packagesspandriver-projects-and-packages"></a><span id="Driver_projects_and_packages"></span><span id="driver_projects_and_packages"></span><span id="DRIVER_PROJECTS_AND_PACKAGES"></span>驱动程序项目和包


驱动程序项目  是一个 Microsoft Visual Studio 项目，它生成驱动程序二进制文件（如 .sys 文件），并有可能生成驱动程序的 INF 文件。

驱动程序包  是用于安装驱动程序的文件集合。 包中包括 INF 文件，以及该 INF 引用的文件和二进制文件。 Visual Studio 使用驱动程序包将驱动程序自动部署到远程目标并进行调试。

驱动程序包是一个单独项目，它从一个或多个项目（如驱动程序项目）收集输出。 驱动程序包项目在生成后即生成 Visual Studio 用于部署驱动程序的驱动程序包。

![visual studio 解决方案资源管理器驱动程序包项目](images/VsSlnExplorer.png)

**注意**  

 

如果使用驱动程序模板创建驱动程序解决方案，则模板应会自动创建包含两个项目的解决方案。 一个用于驱动程序，另一个用于驱动程序包。
## <a name="span-idmanually_creating_a_driver_packagespanspan-idmanually_creating_a_driver_packagespanspan-idmanually_creating_a_driver_packagespanmanually-creating-a-driver-package"></a><span id="Manually_creating_a_driver_package"></span><span id="manually_creating_a_driver_package"></span><span id="MANUALLY_CREATING_A_DRIVER_PACKAGE"></span>手动创建驱动程序包


如果解决方案没有驱动程序包，可以在 Visual Studio 中手动创建一个，方法是从“文件”  菜单选择“新建”&gt;“项目”  。 有关如何创建驱动程序包的示例，请参阅[编写第一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-your-first-driver)。

若要为没有驱动程序包的现有解决方案手动创建一个新的驱动程序包，请使用“驱动程序安装包”模板。 选择“文件”->“新建”->“项目”  。 然后从对话框中选择“Windows 驱动程序”&gt;“包”&gt;“驱动程序安装包”  。 然后在“解决方案”  下拉列表中，选择“添加到解决方案”  ，然后单击“确定”  。

## <a name="span-idmodifying_an_existing_driver_packagespanspan-idmodifying_an_existing_driver_packagespanspan-idmodifying_an_existing_driver_packagespanmodifying-an-existing-driver-package"></a><span id="Modifying_an_existing_driver_package"></span><span id="modifying_an_existing_driver_package"></span><span id="MODIFYING_AN_EXISTING_DRIVER_PACKAGE"></span>修改现有的驱动程序包


如果解决方案已包含驱动程序包，可以将其修改为引用解决方案中的其他项目。

在“解决方案资源管理器”窗格中，打开驱动程序包项目，右键单击“引用”  ，选择“添加引用…”  并选择要引用的项目。

若要删除对现有项目的引用，请右键单击不再需要引用的现有项目，并单击“删除”  。

![驱动程序包属性](images/VsDrvrPkgProps.png)

## <a name="span-idmultiple_drivers_in_a_solutionspanspan-idmultiple_drivers_in_a_solutionspanspan-idmultiple_drivers_in_a_solutionspanmultiple-drivers-in-a-solution"></a><span id="Multiple_drivers_in_a_solution"></span><span id="multiple_drivers_in_a_solution"></span><span id="MULTIPLE_DRIVERS_IN_A_SOLUTION"></span>解决方案中的多个驱动程序


可以将多个驱动程序及其包添加到解决方案。 与“修改现有驱动程序包”类似，可以创建新的驱动程序解决方案，或添加对现有解决方案的引用。 如果解决方案已包含驱动程序包，则可以将其修改为引用解决方案中的其他驱动程序项目。

在“解决方案资源管理器”窗格中，打开驱动程序包项目，右键单击“引用”  ，选择“添加引用…”  并选择要引用的项目。

若要删除对现有项目的引用，请右键单击不再需要引用的现有项目，并单击“删除”  。

有关包含多个驱动程序的单个解决方案的示例，请参阅“Toaster 示例驱动程序”示例：![单个解决方案中的多个驱动程序](images/MultipleDriversSingleSolution.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [签署驱动程序](signing-a-driver.md)
 

 






