---
title: 可移动设备功能概述
description: 可移动设备功能概述
ms.assetid: c6dfb2ac-89a5-40fd-ae9a-1f2800af9ef8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65e92ad0b95132a95afeb3bb60f158cb4042c73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348745"
---
# <a name="overview-of-the-removable-device-capability"></a>可移动设备功能概述


可移动设备功能是一些 (**可移动**) 中设置总线驱动程序**DEVICE_CAPABILITIES**)。

总线驱动程序时 devnode 和所有其子 devnodes 组成可以以物理方式删除，设备断开连接，或计算机正在运行时从其父 devnode 拔出设置 devnode 的可移动设备功能。 通常情况下，devnode 应标记为 devnode 拓扑中最顶层的 devnode 是否可移动。

Devnode 上正确设置了可移动设备功能很重要。 如果总线驱动程序不能为它枚举 devnode 提供容器的 ID，插即用 (PnP) 管理器使用可移动设备功能生成所有 devnodes 枚举设备的容器 ID。

例如，假设单函数设备，如鼠标，连接到通过 USB 计算机。 在这种情况下，USB 总线驱动程序检测到新设备，检测到它是一个 USB 人体学接口设备 (HID)，并创建 USB HID 设备 devnode。 HID devnode 还检测 HID 设备是鼠标和创建符合 hid 标准的鼠标子 devnode。 此时，鼠标已安装并在计算机上正常工作。 这两个新 devnodes 使用独立*驱动程序堆栈*。

作为一般规则，应将设备的最顶层 （父） devnode 设置为可移动，而每个其子 devnodes 不应设置为可移动。 在上一示例中，USB 总线驱动程序设置**可移动**位为**TRUE** USB HID devnode 和集**可移动**位为**FALSE**为子符合 hid 标准的鼠标 devnode。

以下设备管理器屏幕截图显示了泛型 USB 鼠标，devnode 拓扑，并显示鼠标的 devnodes 被标记为可移动。

![显示有关 usb 鼠标 devnode 拓扑的设备管理器窗口的屏幕截图](images/containerid-2.png)

 

 





