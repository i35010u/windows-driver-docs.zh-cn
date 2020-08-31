---
title: 排查容器 ID 实现问题
description: 排查容器 ID 实现问题
ms.assetid: 9c992f5a-73b6-4567-977f-1cd92862bf60
keywords:
- 容器 Id WDK，故障排除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 068123d60c577e1f707ec6a3cd8a09b5dbb72dbe
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095883"
---
# <a name="troubleshooting-the-implementation-of-container-ids"></a>排查容器 ID 实现问题


如果 "设备和打印机" 用户界面中的设备有多个 (UI) 出现，则设备不会正确实现容器 ID 要求。 此不正确的实现会导致即插即用 (PnP) manager 将一个或多个设备节点（ (*devnodes*) 组合到设备的其他设备容器中）。

在这种情况下，应检查以下各项：

-   为设备枚举的每个 devnode 是否正确设置了可移动设备功能？

    这是 "设备和打印机" UI 中多个设备实例的最常见原因。 请确保设备的每个 devnode 都有相应的可移动设备功能设置。 应将设备的最顶层或 *父*devnode 报告为可移动，并且应将其所有子项报告为不可删除。 自定义总线驱动程序实现必须正确分配其所枚举的 devnodes 的可移动关系。

    设备管理器是一种很有用的工具来诊断这些问题。 可以通过执行以下步骤来查看完整的 devnode 层次结构：

    1.  右键单击 " **我的电脑** " 图标，然后单击 " **管理** "。 并从生成的显示中列出的系统工具中选择 **设备管理器** 。
    2.  单击下拉菜单中的 " **按连接查看** "。
    3.  找到构成设备的 devnodes。 对于每个 devnode，右键单击该节点，然后单击 " **属性"。**
    4.  在 " **详细信息** " 选项卡上的 " **属性** " 下拉列表中，单击 " **功能**"。

    如果 devnode 的功能值列表包含 CM_DEVCAP_REMOVABLE 标志，则将 devnode 标记为可移动。 然后，即插即用 (PnP) manager 将为 devnode 及其子节点创建无法删除的新设备容器。

    有关可移动设备功能的详细信息，请参阅 [从可移动设备功能生成的容器 id](container-ids-generated-from-the-removable-device-capability.md)。

    有关设备管理器的详细信息，请参阅 [使用设备管理器](using-device-manager.md)。

-   设备是否在硬件中包含容器 ID 或其他唯一标识符？

    请确保硬件中的容器 ID 或唯一标识符的格式符合给定总线的格式要求。 有关详细信息，请参阅 [从特定于总线的唯一 ID 生成的容器 id](container-ids-generated-from-a-bus-specific-unique-id.md)。

    如果自定义总线驱动程序枚举了设备的 devnodes，请检查总线驱动程序是否正确响应针对**BusQueryContainerID**的[**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md)请求。

-   设备是否通过多个总线并发连接到计算机？

    如果设备通过两个或多个总线并发连接到计算机，则设备和打印机 UI 中会出现两个或两个以上的设备实例。 这些实例可为设备所附加到的每个总线提供一个或多个设备实例。 若要解决此问题，请确保设备报告容器 ID 或设备特定的唯一标识符，并在每个总线上报告相同的值。

 

