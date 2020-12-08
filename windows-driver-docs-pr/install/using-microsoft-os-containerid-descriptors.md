---
title: 使用 Microsoft OS ContainerID 描述符
description: 使用 Microsoft OS ContainerID 描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a457d132e0b1e9eb141fac53d599d8a0691d3d2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827033"
---
# <a name="using-microsoft-os-containerid-descriptors"></a>使用 Microsoft OS ContainerID 描述符


可以在通过多个系统总线支持设备的同时连接的设备中使用 Microsoft 操作系统 (OS) **ContainerID** 描述符。 明确定义的 Microsoft 操作系统 **ContainerID** 描述符确保为 USB 总线上的设备 (*devnodes*) 的所有设备节点都分组到相同的设备容器。

**注意**  如果决定实现 Microsoft 操作系统 **ContainerID** 描述符，则每个设备上的描述符值必须唯一，以避免容器 ID 冲突。

 

如果设备支持通过多个总线同时连接到设备，则可以使用 Microsoft 操作系统 **ContainerID** 描述符。 这样，就会在设备支持的每个总线上使用相同的容器 ID。 这允许操作系统确定每个总线上的函数是否属于同一设备容器。

如果决定使用 USB 设备中的 Microsoft 操作系统 **ContainerID** ，应注意以下几点：

-   对于未集成到计算机的设备 (即) 的所有外部设备，最佳做法是始终在 USB 设备硬件中提供 Microsoft 操作系统 **ContainerID** 描述符和序列号。 这将确保 Windows 即插即用 (PnP) 基础结构能够正确地将设备公开的所有设备功能组合在一起。 从 Windows 7 开始，操作系统的组件依赖于正确的设备功能分组。 按照此做法，可以为 Windows 平台上的设备提供最佳用户体验。

-   与计算机集成的 USB 设备决不应提供 Microsoft 操作系统 **ContainerID** 描述符。 为了确保集成设备与计算机的设备容器正确组合，集成设备应依赖于 ACPI BIOS 设置，或适用于端口的 USB 集线器描述符 **DeviceRemovable** 位。

 

 





