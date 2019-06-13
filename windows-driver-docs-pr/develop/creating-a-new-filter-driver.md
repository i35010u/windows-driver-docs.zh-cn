---
ms.assetid: AB4E6021-FDF9-40D0-818C-9602E1AEA564
title: 创建新的筛选器驱动程序
description: 在本主题中，我们将介绍如何使用 Visual Studio 开始编写新的筛选器驱动程序。 筛选器驱动程序不同于设备功能驱动程序、软件驱动程序和文件系统驱动程序，这些驱动程序我们将在其他主题中加以介绍。
keywords: 筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d6807e13500558450dafd4be1f37989cc956c45
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63382415"
---
# <a name="creating-a-new-filter-driver"></a>创建新的筛选器驱动程序

在本主题中，我们将介绍如何使用 Visual Studio 开始编写新的筛选器驱动程序。 筛选器驱动程序不同于设备功能驱动程序、软件驱动程序和文件系统驱动程序，这些驱动程序我们将在其他主题中加以介绍。 若要了解筛选器驱动程序以及它们与其他类型的驱动程序有何不同，请参阅以下主题。

-   [什么是驱动程序？](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554678)
-   [选择驱动程序模型](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554652)
-   [设备节点和设备堆栈](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554721)
-   [筛选器驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545890)
-   [WDM 驱动程序的类型](https://msdn.microsoft.com/Library/Windows/Hardware/Ff564862)

开始之前，请先确定哪个驱动程序模型适用于你的筛选器驱动程序。 如果在确定最适合的模型时需要帮助，请参阅[选择驱动程序模型](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554652)。 如果要为硬件设备编写筛选器驱动程序，请确定设备适合位于[设备和驱动程序技术](https://msdn.microsoft.com/Library/Windows/Hardware/Ff557557)中介绍的技术列表的哪个位置。 请参阅该特定技术的相关文档，了解是否有关于选择筛选器驱动程序模型的任何指南。 建议的筛选器驱动程序模型因技术而异。 对于有些技术，此文档建议使用用户模式驱动程序框架 (UMDF)、内核模式驱动程序框架 (KMDF) 或 Windows 驱动程序模型 (WDM)。 对于其他技术，此文档为如何编写筛选器驱动程序提供了明确的详细信息。 部分技术有微筛选器模型。 对于有些技术，可能没有任何针对筛选器驱动程序模型的建议。

接下来，确定以下哪个案例介绍你的驱动程序模型建议，并按照步骤进行操作：

## <a name="span-idcase1thedocumentationforyourtechnologyrecommendsumdfspanspan-idcase1thedocumentationforyourtechnologyrecommendsumdfspancase-1-the-documentation-for-your-technology-recommends-umdf"></a><span id="case_1__the_documentation_for_your_technology_recommends_umdf."></span><span id="CASE_1__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_UMDF."></span>案例 1：你的技术的文档建议使用 UMDF。


1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在“新建项目”对话框的左侧窗格中，找到并选择“Visual C++ | Windows 驱动程序 | WDF”  。
3.  在中间窗格中，选择“用户模式驱动程序(UMDF)”  。
4.  填写“名称”  和“位置”  框，然后单击“确定”  。 有关详细信息，请参阅[基于模板编写 UMDF 驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439659)。
    **注意**  在创建新的 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。
5.  此时，你的驱动程序项目可以实现大多数 UMDF 驱动程序所需的一般代码。 现在你可以提供特定于你的筛选器的代码。

## <a name="span-idcase2thedocumentationforyourtechnologyrecommendskmdfspanspan-idcase2thedocumentationforyourtechnologyrecommendskmdfspancase-2-the-documentation-for-your-technology-recommends-kmdf"></a><span id="case_2__the_documentation_for_your_technology_recommends_kmdf."></span><span id="CASE_2__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_KMDF."></span>案例 2：你的技术的文档建议使用 KMDF。


1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在“新建项目”对话框的左侧窗格中，找到并选择“WDF”  。
3.  在中间窗格中，选择“内核模式驱动程序(KMDF)”  。
4.  填写“名称”  和“位置”  框，然后单击“确定”  。 有关详细信息，请参阅[基于模板编写 KMDF 驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)。
    **注意**  在创建新的 KMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。
5.  此时，你的驱动程序项目可以实现大多数 KMDF 驱动程序所需的一般代码。 现在你可以提供特定于你的筛选器的代码。

## <a name="span-idcase3thedocumentationforyourtechnologydescribesaspecificfilterorminifiltermodelspanspan-idcase3thedocumentationforyourtechnologydescribesaspecificfilterorminifiltermodelspancase-3-the-documentation-for-your-technology-describes-a-specific-filter-or-mini-filter-model"></a><span id="case_3__the_documentation_for_your_technology_describes_a_specific_filter_or_mini_filter_model."></span><span id="CASE_3__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_DESCRIBES_A_SPECIFIC_FILTER_OR_MINI_FILTER_MODEL."></span>案例 3：你的技术的文档介绍特定筛选器或微筛选器模型。


如果你的设备技术具有特定的筛选器或微筛选器模型，请查看 Visual Studio 是否具有该模型的模板。

1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在“新建项目”对话框的左侧窗格中，找到并选择“模板 | Visual C++ | Windows 驱动程序”  。
3.  浏览已安装模板列表，查看是否有你需要编写的筛选器类型的模板。 例如，可以选择“筛选器驱动程序:  NDIS”模板（在**网络**下）。
4.  如果 **Windows 驱动程序**下没有你的筛选器驱动程序类型的模板，请单击“联机”  并浏览联机可用的模板。
5.  如果你找到了你的筛选器驱动程序类型的模板，请选择该模板，填写“名称”  和“位置”  框，然后单击“确定”  。
6.  此时，你的驱动程序项目可以实现筛选器驱动程序所需的一般代码。 现在你可以提供特定于你的筛选器的代码。 请参阅你的技术的文档来了解你需要实现的功能。

如果你的设备技术有特定的筛选器模型或微筛选器模型，并且你找不到你的筛选器驱动程序类型的模板，请参阅技术特定文档获取确定是使用 UMDF、KMDF 还是使用 WDM 的指导信息。

## <a name="span-idcase4thedocumentationforyourtechnologyrecommendswdmspanspan-idcase4thedocumentationforyourtechnologyrecommendswdmspancase-4-the-documentation-for-your-technology-recommends-wdm"></a><span id="case_4__the_documentation_for_your_technology_recommends_wdm."></span><span id="CASE_4__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_WDM."></span>案例 4：你的技术的文档建议使用 WDM。


1.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2.  在 Visual Studio 中的“新建项目”对话框中，在“Windows 驱动程序”  下选择 **WDM**。
3.  填写“名称”  和“位置”  框，然后单击“确定”  。
4.  此时，你有一个空的 WDM 驱动程序项目。 在“解决方案资源管理器”窗口中，右键单击你的驱动程序项目，然后选择“添加 | 新项目”  。
5.  在“添加新项目”对话框中，选择“C++ 文件(.cpp)”  ，为文件输入一个名称，然后单击“确定”  。

    **注意**  如果你想要创建 .c 文件，而不是 .cpp 文件，请输入具有 **.c** 扩展名的名称。
6.  实现你的筛选器所需的功能。 在实现和组织功能时，你可能决定添加其他 .cpp 或 .c 文件。

## <a name="span-idcase5thedocumentationforyourtechnologydoesnothavearecommendationforafilterdrivermodelspanspan-idcase5thedocumentationforyourtechnologydoesnothavearecommendationforafilterdrivermodelspancase-5-the-documentation-for-your-technology-does-not-have-a-recommendation-for-a-filter-driver-model"></a><span id="case_5__the_documentation_for_your_technology_does_not_have_a_recommendation_for_a_filter_driver_model."></span><span id="CASE_5__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_DOES_NOT_HAVE_A_RECOMMENDATION_FOR_A_FILTER_DRIVER_MODEL."></span>案例 5：你的技术的相关文档未提供针对筛选器驱动程序模型的建议。


1.  确定 UMDF、KMDF 或 WDM 是否是最适合你的筛选器驱动程序的模型。 如需帮助，请参阅[选择驱动程序模型](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554652)。
2.  在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
3.  在 Visual Studio 的“新建项目”对话框中，在“Windows 驱动程序”  下，选择以下模板之一：

    -   **WDF | 用户模式驱动程序 (UMDF)**
    -   **WDF | 内核模式驱动程序 (KMDF)**
    -   **WDM | 空内核驱动程序**

    **注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。
4.  实现你的筛选器所需的功能。 根据需要创建新的 .c 或 .cpp 文件。

如果你不确定要使用哪个模板，请考虑阅读 [Windows 硬件 WDK 和驱动程序开发](https://go.microsoft.com/fwlink/p?LinkID=252169)论坛帖子或将问题发布到论坛中。

 

 



