---
title: 如何从可移动设备功能生成容器 Id
description: 如何通过可移动设备功能生成容器 ID
ms.assetid: 493a9473-4989-4557-b2b2-efa0e2a8b24e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aaae8db2d5bbcbd1c7103d93f0aed3ee19d728e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325822"
---
# <a name="how-container-ids-are-generated-from-the-removable-device-capability"></a>如何通过可移动设备功能生成容器 ID


如果总线驱动程序不能提供的设备节点的容器 ID (*devnode*)，它枚举，插即用 (PnP) 管理器使用可移动设备功能来生成所有 devnodes 枚举设备的容器 ID。 有关可移动设备功能的详细信息，请参阅[可移动设备功能的概述](overview-of-the-removable-device-capability.md)。

下面启发式方法介绍了如何从可移动设备功能生成的容器 Id:

1.  Devnode 是否可移动设备功能设置为 **，则返回 TRUE**，生成 devnode 的新容器 ID。

2.  Devnode 是否可移动设备功能设置为**FALSE**，继承其父 devnode 容器 ID。

Devnode 无法枚举子 devnodes，直到它被初始化并将其*驱动程序堆栈*已启动。 只要在初始化过程中分配其容器 ID，devnode 已准备好这些枚举传播到任何子项不可删除其容器 ID。

使用可移动设备功能设置为 devnode **，则返回 TRUE**被视为最顶层 （父） devnode 的设备，并为此 devnode 生成 ID 的容器。

此父 devnode 的所有子级都继承相同的容器 ID，除非他们自己拥有其可移动设备功能设置为 **，则返回 TRUE**。 在这种情况下，可移动子 devnode 分配不同的容器 ID，并将成为此可移动设备的父 devnode。 该 devnode 的所有子级都继承相同的容器 id。

例如，假设单函数鼠标连接到通过 USB 的计算机。 在这种情况下，USB 总线驱动程序检测到新设备，并检测它是一个 USB 人体学接口设备 (HID)。 然后，USB 总线驱动程序创建 USB HID 设备 devnode。 HID devnode 还检测 HID 设备是鼠标和创建符合 hid 标准的鼠标子 devnode

将此启发式方法应用于此示例会导致以下操作：

1.  创建 USB HID devnode。 可移动设备功能设置为 **，则返回 TRUE**上此 devnode 因为其父 USB 集线器 devnode 识别它被插入到面向外部的 USB 端口。

2.  因为它是可移动设备的最顶层的 devnode，为此 devnode 创建容器 ID。 因此，此 devnode 被视为父 devnode 为可移动设备。

3.  创建符合 hid 标准的鼠标 devnode。 可移动设备功能设置为**FALSE**上此 devnode 因为其父 USB HID devnode 报告其所有子级用作不可删除。 在这种情况下，符合 hid 标准的鼠标 devnode 继承父 devnode 的容器 ID。

此启发式方法，通过相同的容器 ID 分配给每个 devnode 属于鼠标。 PnP 管理器成功分组 devnodes 到逻辑设备，即使设备没有唯一标识符。

**请注意**  此启发式方法的成功依赖于正确地报告它枚举每个 devnode 的可移动设备功能特定的总线驱动程序。 总线驱动程序必须确保设备的父 devnode 应设置为可移动，并其子 devnodes 不应设置为可移动。

 

 

 





