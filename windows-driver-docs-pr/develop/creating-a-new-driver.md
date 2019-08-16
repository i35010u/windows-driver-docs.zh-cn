---
ms.assetid: A637B75C-C227-495A-AB5B-B42DDF7842B9
title: 创建新设备功能驱动程序
description: 在本主题中，我们将介绍如何使用 Visual Studio 开始编写新的设备功能驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d023d9883cb92acd21636a7ff89f73a926c0b65f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370789"
---
# <a name="creating-a-new-device-function-driver"></a>创建新设备功能驱动程序

在本主题中，我们将介绍如何使用 Visual Studio 开始编写新的设备功能驱动程序。 设备功能驱动程序不同于筛选器驱动程序、软件驱动程序和文件系统驱动程序，这些驱动程序我们将在其他主题中加以介绍。 若要了解设备功能驱动程序以及它们与其他类型的驱动程序有何不同，请参阅[驱动程序是什么？](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/what-is-a-driver-)、[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)和[设备节点与设备堆栈](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)。

若要开始，请先确定设备适合位于[设备和驱动程序技术](https://docs.microsoft.com/windows-hardware/drivers/)中介绍的技术列表的哪个位置。 若要了解哪些驱动程序模型可用于你的设备，请参阅该特定技术的文档。 推荐的驱动程序模型因技术而异。 对于有些技术，此文档建议使用“用户模式驱动程序框架 (UMDF)”或“内核模式驱动程序框架 (KMDF)”。 对于其他技术，该文档介绍了如何创建属于驱动程序对的微型驱动程序。 微型驱动程序有各种名称，包括微型端口和微型类。

接下来，确定以下哪个案例介绍你的驱动程序模型建议，并按照步骤进行操作：

### <a name="span-idcase_1__the_documentation_for_your_technology_recommends_umdfspanspan-idcase_1__the_documentation_for_your_technology_recommends_umdfspanspan-idcase_1__the_documentation_for_your_technology_recommends_umdfspancase-1-the-documentation-for-your-technology-recommends-umdf"></a><span id="Case_1__The_documentation_for_your_technology_recommends_UMDF."></span><span id="case_1__the_documentation_for_your_technology_recommends_umdf."></span><span id="CASE_1__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_UMDF."></span>案例 1：你的技术的文档建议使用 UMDF。

1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在“新建项目”对话框的左侧窗格中，找到并选择“Visual C++ | Windows 驱动程序 | WDF”  。
3.  在中间窗格中，选择“用户模式驱动程序(UMDF)”  。
4.  填写“名称”  和“位置”  框，然后单击“确定”  。 有关详细信息，请参阅[基于模板编写 UMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-umdf-driver-based-on-a-template)。
    **注意**  在创建新的 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。
5.  此时，你的驱动程序项目可以实现大多数 UMDF 驱动程序所需的一般代码。 现在你可以提供特定于你的设备的代码。 请参阅你的技术的相关文档来了解你需要实现的接口。

### <a name="span-idcase_2__the_documentation_for_your_technology_recommends_kmdfspanspan-idcase_2__the_documentation_for_your_technology_recommends_kmdfspanspan-idcase_2__the_documentation_for_your_technology_recommends_kmdfspancase-2-the-documentation-for-your-technology-recommends-kmdf"></a><span id="Case_2__The_documentation_for_your_technology_recommends_KMDF."></span><span id="case_2__the_documentation_for_your_technology_recommends_kmdf."></span><span id="CASE_2__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_KMDF."></span>案例 2：你的技术的文档建议使用 KMDF。

1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在“新建项目”对话框的左侧窗格中，找到并选择“WDF”  。
3.  在中间窗格中，选择“内核模式驱动程序(KMDF)”  。
4.  填写“名称”  和“位置”  框，然后单击“确定”  。 有关详细信息，请参阅[基于模板编写 KMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)。
    **注意**  在创建新的 KMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。
5.  此时，你的驱动程序项目可以实现大多数 KMDF 驱动程序所需的一般代码。 现在你可以提供特定于你的设备的代码。 请参阅你的技术的相关文档来了解你需要实现的方法。

### <a name="span-idcase_3__the_documentation_for_your_technology_describes_a_minidriver_modelspanspan-idcase_3__the_documentation_for_your_technology_describes_a_minidriver_modelspanspan-idcase_3__the_documentation_for_your_technology_describes_a_minidriver_modelspancase-3-the-documentation-for-your-technology-describes-a-minidriver-model"></a><span id="Case_3__The_documentation_for_your_technology_describes_a_minidriver_model."></span><span id="case_3__the_documentation_for_your_technology_describes_a_minidriver_model."></span><span id="CASE_3__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_DESCRIBES_A_MINIDRIVER_MODEL."></span>案例 3：你的技术的相关文档介绍了微型驱动程序模型。

如果你的设备技术具有微型端口、微型类或某种其他类型的微型驱动程序模型，请查看 Visual Studio 是否具有该模型的特定模板。

1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在“新建项目”对话框的左侧窗格中，找到并选择“模板 | Visual C++ | Windows 驱动程序”  。
3.  浏览已安装模板列表，查找你需要编写的微型驱动程序类型的模板。
4.  如果 **Windows 驱动程序**下没有你的微型驱动程序类型的模板，请单击“联机”  并浏览联机可用的模板。
5.  如果你找到了你的微型驱动程序类型的模板，请选择该模板，填写“名称”  和“位置”  框，然后单击“确定”  。
6.  此时，你的驱动程序项目可以实现微型驱动程序所需的一般代码。 现在你可以提供特定于你的设备的代码。 请参阅你的技术的文档来了解你需要实现的功能。

如果你的设备技术具有微型驱动程序模型，并且你找不到你的微型驱动程序类型的特定模板，Windows 驱动程序模型 (WDM) 模板最有可能成为你的起点。 请参阅技术特定文档获取指导信息。 在极少数情况下，你可以使用 KMDF 编写微型驱动程序，但通常起点是 WDM。

1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在 Visual Studio 中的“新建项目”对话框中，在“Windows 驱动程序”  下选择 **WDM**。
3.  填写“名称”  和“位置”  框，然后单击“确定”  。
4.  此时，你有一个空的 WDM 驱动程序项目。 在“解决方案资源管理器”窗口中，右键单击你的驱动程序项目，然后选择“添加 | 新项目”  。
5.  在“添加新项目”对话框中，选择“C++ 文件(.cpp)”  ，为文件输入一个名称，然后单击“确定”  。

    **注意**  如果你想要创建 .c 文件，而不是 .cpp 文件，请输入具有 **.c** 扩展名的名称。
6.  请参阅你的技术的文档来了解你需要实现的功能。 在实现和组织功能时，你可能决定添加其他 .cpp 或 .c 文件。

 

 





