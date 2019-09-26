---
title: 可移动设备功能概述
description: 可移动设备功能概述
ms.assetid: c6dfb2ac-89a5-40fd-ae9a-1f2800af9ef8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f474224ee7849f3bde6bb24c3f2ee2460d8717
ms.sourcegitcommit: 8d45beff38c5d3b695eadbf624b6726c797d9b97
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271980"
---
# <a name="overview-of-the-removable-device-capability"></a>可移动设备功能概述


可移动设备功能是总线驱动程序在**DEVICE_CAPABILITIES**中设置的一个位（**可移动**）。

当计算机正在运行时，总线驱动程序会为 devnode 设置可移动设备功能，并在 devnode 及其所有子 devnodes 组成设备时，该设备可以物理删除、断开连接或从其父 devnode 中拔出。 通常，如果 devnode 是 devnode 拓扑中最顶层的 devnode，则应将其标记为可移动。

在 devnode 上正确设置可移动设备功能很重要。 如果总线驱动程序无法为其枚举的 devnode 提供容器 ID，则即插即用（PnP）管理器使用可移动设备功能为该设备的所有 devnodes 枚举生成容器 ID。

例如，假设单一功能设备（如鼠标）通过 USB 连接到计算机。 在这种情况下，USB 总线驱动程序检测到新设备，检测到它是 USB 人体学接口设备（HID），并为该设备创建 USB HID devnode。 HID devnode 还检测到 HID 设备是一个鼠标，并为符合 HID 标准的鼠标创建子 devnode。 此时，鼠标已安装，并且在计算机上正常运行。 这两个新的 devnodes 使用独立的*驱动程序堆栈*。

作为一般规则，设备的最顶层（父） devnode 应设置为可移动，而其每个子 devnodes 不应设置为可移动。 在上面的示例中，USB 总线驱动程序将 USB HID devnode 的 "**可移动**" 设置为 " **TRUE** "，并将 "**可移动**位" 设置为 " **FALSE** " （对于子 hid 兼容的鼠标 devnode）。

以下设备管理器屏幕截图显示了通用 USB 鼠标的 devnode 拓扑，并显示了哪些 devnodes 标记为可移动。

![显示 usb 鼠标的 devnode 拓扑的 "设备管理器" 窗口的屏幕截图](images/containerid-2.png)

 

 





