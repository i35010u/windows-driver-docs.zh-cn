---
ms.assetid: AB35CE97-0C66-47B3-9C64-81BA01D65104
title: 创建新的软件驱动程序
description: 在本主题中，我们将介绍如何使用 Visual Studio 开始编写新的软件驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bcaf5c2e7e27eb5d4791f6825f9a7412768123e3
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67370774"
---
# <a name="creating-a-new-software-driver"></a>创建新的软件驱动程序

在本主题中，我们将介绍如何使用 Visual Studio 开始编写新的软件驱动程序。 软件驱动程序不同于设备功能驱动程序、筛选器驱动程序和文件系统驱动程序，这些驱动程序我们将在其他主题中加以介绍。 有关软件驱动程序以及它们与其他类型的驱动程序有何不同的详细信息，请参阅[什么是驱动程序？](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/what-is-a-driver-)和[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。

开始之前，请先确定哪个驱动程序模型适用于你的软件驱动程序。 三个选项分别是内核模式驱动程序框架 (KMDF)、旧 NT 驱动程序模型和 Windows 驱动程序模型 (WDM)。 如果在确定最适合的模型时需要帮助，请参阅[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。

## <a name="case-1-you-want-to-use-kmdf"></a>案例 1：你想要使用 KMDF

1. 在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2. 在“新建项目”对话框的左侧窗格中，找到并选择“WDF”  。
3. 在中间窗格中，选择“内核模式驱动程序(KMDF)”  。
4. 填写“名称”  和“位置”  框，然后单击“确定”  。 有关详细信息，请参阅[基于模板编写 KMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)。
    > [!NOTE]
    > 在创建新的 KMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。
5. 此时，你的驱动程序项目可以实现大多数 KMDF 驱动程序所需的一般代码。 现在你可以提供特定于你的软件驱动程序的代码。

## <a name="case-2-you-want-to-use-the-legacy-nt-model"></a>情况 2：你想要使用传统的 NT 模型

1. 在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2. 在 Visual Studio 的“新建项目”对话框中，在“Windows 驱动程序”  下选择“WDM | 空 WDM 驱动程序”  。

    > [!NOTE]
    > 不需要编写 WDM 驱动程序，但需要“空 WDM 驱动程序”  模板。
3. 填写“名称”  和“位置”  框，然后单击“确定”  。
4. 此时，你有一个空的 WDM 驱动程序项目。 在“解决方案资源管理器”窗口中，右键单击你的驱动程序项目，然后选择“添加 | 新项目”  。
5. 在“添加新项目”对话框中，选择“C++ 文件(.cpp)”  ，为文件输入一个名称，然后单击“确定”  。

    > [!NOTE]
    > 若要创建 .c 文件而不是 .cpp 文件，请输入包含 **.c** 扩展名的名称。
6. 包括 ntddk.h。
7. 实现你的软件驱动程序所需的功能。 在实现和组织功能时，你可能决定添加头文件和其他 .cpp 或 .c 文件。

## <a name="case-3-you-want-to-use-wdm"></a>情况 3：你想要使用 WDM

你想要对软件驱动程序使用 WDM 的可能性微乎其微。 但如果你有此打算，请执行以下步骤。

1. 在 Visual Studio 中的“文件”  菜单上，选择“新建 | 项目”  。
2. 在 Visual Studio 中的“新建项目”对话框中，在“Windows 驱动程序”  下选择 **WDM**。
3. 填写“名称”  和“位置”  框，然后单击“确定”  。
4. 此时，你有一个空的 WDM 驱动程序项目。 在“解决方案资源管理器”窗口中，右键单击你的驱动程序项目，然后选择“添加 | 新项目”  。
5. 在“添加新项目”对话框中，选择“C++ 文件(.cpp)”  ，为文件输入一个名称，然后单击“确定”  。

    > [!NOTE]
    > 若要创建 .c 文件而不是 .cpp 文件，请输入包含 **.c** 扩展名的名称。
6. 包括 wdm.h。
7. 实现你的软件驱动程序所需的功能。 在实现和组织功能时，你可能决定添加头文件和其他 .cpp 或 .c 文件。
