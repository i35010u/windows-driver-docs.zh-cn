---
title: 如何从可移动设备功能生成容器 Id
description: 如何通过可移动设备功能生成容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a04f735c0e9db55fed6f51f3a12d08b574d9eaa1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791737"
---
# <a name="how-container-ids-are-generated-from-the-removable-device-capability"></a>如何通过可移动设备功能生成容器 ID


如果总线驱动程序无法为其枚举 (*devnode*) 的设备节点提供容器 id，即插即用 (PnP) manager 将使用可移动设备功能为该设备的所有 devnodes 枚举生成容器 id。 有关可移动设备功能的详细信息，请参阅 [可移动设备功能的概述](overview-of-the-removable-device-capability.md)。

以下试探法介绍了如何从可移动设备功能生成容器 Id：

1.  如果 devnode 将可移动设备功能设置为 **TRUE**，则为 devnode 生成新的容器 ID。

2.  如果 devnode 将可移动设备功能设置为 **FALSE**，则会从其父 devnode 继承容器 ID。

Devnode 无法枚举子 devnodes，直到它被初始化并启动其 *驱动程序堆栈* 。 在初始化期间，一旦分配其容器 ID，devnode 就可以将其容器 ID 向下传播到其在枚举时的任何不可移动子级。

将可移动设备功能设置为 **TRUE** 的 devnode 被视为设备的最顶层 (父) devnode，并为此 devnode 生成容器 ID。

此父 devnode 的所有子级都将继承相同的容器 ID，除非它们本身将其可移动设备功能设置为 **TRUE**。 在这种情况下，会向可移动子 devnode 分配一个不同的容器 ID，并成为该可移动设备的父 devnode。 该 devnode 的所有子级继承相同的容器 ID。

例如，假设单功能鼠标通过 USB 连接到计算机。 在这种情况下，USB 总线驱动程序检测到一个新设备，并检测到它是一个 (HID) 的 USB 人体学接口设备。 然后，USB 总线驱动程序会为设备创建 USB HID devnode。 HID devnode 还检测到 HID 设备是一个鼠标，并为符合 HID 标准的鼠标创建子 devnode

将此试探法应用于此示例将导致以下操作：

1.  已创建 USB HID devnode。 此 devnode 上的可移动设备功能设置为 **TRUE** ，因为它的父 USB 集线器 devnode 识别了它已插入到面向外部的 usb 端口中。

2.  为此 devnode 创建容器 ID 是因为它是可移动设备的最顶层 devnode。 因此，此 devnode 被视为可移动设备的父 devnode。

3.  创建与 HID 兼容的鼠标 devnode。 在此 devnode 上，可移动设备功能设置为 **FALSE** ，因为其父 USB HID devnode 将其所有子级报告为不可移动。 在这种情况下，符合 HID 标准的鼠标 devnode 继承父 devnode 的容器 ID。

通过此试探法，相同的容器 ID 会分配给属于鼠标的每个 devnode。 PnP 管理器已成功将 devnodes 分组为逻辑设备，即使设备没有唯一标识符。

**注意**  此试探法的成功依赖于特定的总线驱动程序，该驱动程序可为其枚举的每个 devnode 正确报告可移动设备功能。 总线驱动程序必须确保将设备的父 devnode 设置为可移动设备，并且其子 devnodes 不应设置为可移动。

 

 

 





