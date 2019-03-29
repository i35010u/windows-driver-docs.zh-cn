---
title: 使用 Microsoft OS ContainerID 描述符
description: 使用 Microsoft OS ContainerID 描述符
ms.assetid: e51b1bc8-fd9d-40f9-b2ae-9f5886f57c7b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 194c94c2516d6083a40d6339d2626ef99f426b35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567723"
---
# <a name="using-microsoft-os-containerid-descriptors"></a>使用 Microsoft OS ContainerID 描述符


Microsoft 操作系统 (OS) **ContainerID**描述符可用于支持通过多个系统总线的设备的同时连接的设备。 显式定义的 Microsoft 操作系统**ContainerID**描述符可以确保设备的所有节点 (*devnodes*) 枚举的 USB 总线上的设备分组到同一设备容器。

**请注意**  如果你决定实现 Microsoft 操作系统**ContainerID**描述符，描述符值必须是唯一以避免容器 ID 冲突的每个设备上。

 

Microsoft OS **ContainerID**描述符时，可以在设备支持同时连接多个总线通过向设备。 这样一来，设备支持的每个总线上使用相同的容器 ID。 这允许操作系统以确定每个总线上的函数是否是相同的设备容器的一部分。

如果您决定使用 Microsoft OS **ContainerID**中您的 USB 设备，你应注意以下几点：

-   对于未集成到计算机 （即，所有外部设备） 的设备，它是始终提供 Microsoft 操作系统的最佳做法**ContainerID**描述符和 USB 设备硬件序列号。 这将确保 Windows 即插即用和播放 (PnP) 基础结构能够正确组由设备公开的所有设备功能。 组件的操作系统从 Windows 7 开始，依赖于设备功能的适当的分组。 遵循此做法将提供在 Windows 平台上设备的最佳用户体验。

-   与计算机集成在一起的 USB 设备应永远不会提供 Microsoft OS **ContainerID**描述符。 若要确保集成的设备与计算机的设备容器进行正确分组，集成的设备应依赖 ACPI BIOS 设置或 USB 集线器描述符**DeviceRemovable**位的端口。

 

 





