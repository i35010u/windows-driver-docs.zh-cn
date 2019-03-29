---
title: 支持 USB 设备上的容器 ID 的最佳做法
description: 支持 USB 设备上的容器 ID 的最佳做法
ms.assetid: 58086d52-196f-4ea3-9ce6-62d3fcb43f9e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e971f39e21b655de026db86486e14f17838a6aa9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565703"
---
# <a name="best-practices-for-supporting-container-ids-on-usb-devices"></a>支持 USB 设备上的容器 ID 的最佳做法


启发式方法，用于生成 USB 设备节点的容器 ID (*devnode*)，其中中介绍过[如何 USB 设备是分配容器 Id](how-usb-devices-are-assigned-container-ids.md)、 很复杂，并且依赖于来自信息多个源。

从 Windows 7 开始，此部分中讨论的建议，应遵循以允许操作系统正确确定设备容器并为你的设备提供最佳用户体验。

本部分包括以下主题讨论了这些建议：

[使用 Microsoft OS ContainerID 描述符](using-microsoft-os-containerid-descriptors.md)

[使用 USB 可移动功能的设备容器分组](using-the-usb-removable-capability-for-device-container-grouping.md)

[避免设备容器冲突](avoiding-device-container-conflicts.md)

 

 





