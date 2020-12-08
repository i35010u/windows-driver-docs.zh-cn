---
title: 支持 USB 设备上的容器 ID 的最佳做法
description: 支持 USB 设备上的容器 ID 的最佳做法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42e2de9ed6b0532bd661dfae80ec98edbcb39d8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783179"
---
# <a name="best-practices-for-supporting-container-ids-on-usb-devices"></a>支持 USB 设备上的容器 ID 的最佳做法


用于生成 USB 设备节点的容器 ID (*devnode*) 的试探法，在 [如何为 Usb 设备分配容器 id](how-usb-devices-are-assigned-container-ids.md)中进行了讨论，它非常复杂，并且依赖于从多个源获取的信息。

从 Windows 7 开始，应遵循本部分中讨论的建议，以允许操作系统正确确定设备容器并为设备提供最佳用户体验。

本部分包含以下主题，其中介绍了这些建议：

[使用 Microsoft OS ContainerID 描述符](using-microsoft-os-containerid-descriptors.md)

[将 USB 可移动功能用于设备容器分组](using-the-usb-removable-capability-for-device-container-grouping.md)

[避免设备容器冲突](avoiding-device-container-conflicts.md)

 

 





