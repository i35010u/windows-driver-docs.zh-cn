---
title: 故障排除容器 Id 的实现
description: 故障排除容器 Id 的实现
ms.assetid: 9c992f5a-73b6-4567-977f-1cd92862bf60
keywords:
- 容器 Id WDK 故障排除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 165189d318d5065d594cf721a9b0c958e536bdf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545809"
---
# <a name="troubleshooting-the-implementation-of-container-ids"></a>故障排除容器 Id 的实现


如果预期只有一个时，将显示多个设备在设备和打印机用户界面 (UI) 的实例，该设备未正确实现容器 ID 要求。 此实现不正确会导致 Plug and Play (PnP) 管理器以一个或多个设备节点进行分组 (*devnodes*) 到设备的其他设备容器。

在这种情况下，应检查以下各项：

-   可移动设备功能为正确设置设备枚举每个 devnode？

    这是在设备和打印机 UI 中的多个设备实例的最常见原因。 请确保设备的每个 devnode 具有适当地设置了可移动设备功能。 最顶层，或*父*、 devnode 设备应报告为可移动，并且其所有子项应都报告为不可移动。 自定义总线驱动程序实现必须将它们枚举 devnodes 可移动关系正确分配。

    设备管理器是一个重要的工具来诊断这些问题。 你可以通过执行以下步骤检查完整 devnode 层次结构：

    1.  右键单击**我的电脑**图标，，然后单击**管理**。 然后选择**设备管理器**系统工具列出生成的显示。
    2.  单击**按连接查看**从下拉列表菜单。
    3.  找到 devnodes 构成你的设备。 对于每个 devnode 中，右键单击该节点，然后单击**属性。**
    4.  上**详细信息**选项卡上，在**属性**下拉列表中，单击**功能**。

    如果 devnode 的功能值的列表包含 CM_DEVCAP_REMOVABLE 标志，devnode 标记为可移动。 插即用 (PnP) 管理器然后创建新的设备容器为 devnode 不能删除及其子级。

    有关可移动设备功能的详细信息，请参阅[从可移动设备功能生成的容器 Id](container-ids-generated-from-the-removable-device-capability.md)。

    有关设备管理器的详细信息，请参阅[使用设备管理器](using-device-manager.md)。

-   容器 ID 或其他唯一标识符的硬件中是否包含设备？

    请确保容器 ID 或硬件中的唯一标识符的格式符合给定的总线的格式要求。 有关详细信息，请参阅[从特定于总线的唯一 ID 生成的容器 Id](container-ids-generated-from-a-bus-specific-unique-id.md)。

    如果设备 devnodes 枚举由自定义总线驱动程序，请检查总线驱动程序的正确响应[ **IRP_MN_QUERY_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)请求**BusQueryContainerID**.

-   设备同时连接到计算机的多个总线？

    如果设备同时通过两个或多个总线连接到计算机，该设备的两个或多个实例可以出现在设备和打印机用户界面。 这些实例可以有一个或多个设备附加到每个总线的设备实例。 若要解决此问题，请确保设备报告的容器 ID 或特定于设备的唯一标识符，每条总线上的报表相同的值。

 

 





