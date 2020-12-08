---
title: USB 3.0 数据结构
description: 本主题介绍 USB 3.0 主机控制器驱动程序使用的数据结构。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 538ad0ca0b8d584157d5e4cf3d0fbe187a42777e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803247"
---
# <a name="usb-30-data-structures"></a>USB 3.0 数据结构

本主题介绍 USB 3.0 主机控制器驱动程序使用的数据结构。 了解这些数据结构可帮助你有效地使用 [USB 3.0](usb-3-extensions.md) 和 [RCDRKD](rcdrkd-extensions.md) 调试器扩展命令。 此处提供的数据结构具有与 [USB 3.0 规范](https://www.usb.org/documents)一致的名称。 熟悉 USB 3.0 规范将进一步增强使用扩展命令调试 USB 3.0 驱动程序的能力。

USB 3.0 主机控制器驱动程序是 USB 3.0 核心驱动程序堆栈的一部分。 有关详细信息，请参阅 [USB 驱动程序堆栈体系结构](../usbcon/usb-3-0-driver-stack-architecture.md)。

每个 USB 3.0 主机控制器最多可包含255个设备，每个设备最多可以有31个终结点。 下图显示了一些表示一个主机控制器和连接的设备的数据结构。

![usb 3.0 数据结构，它表示一个主机控制器和连接的设备，这些设备的设备上下文依次为槽和终结点上下文](images/usb3structures01.png)

## <a name="device-context-base-array"></a>设备上下文基数组

设备上下文基数组是指向设备上下文结构的指针的数组。 连接到主机控制器的每个设备都有一个设备上下文结构。 元素1到255指向设备上下文结构。 元素0指向主机控制器的上下文结构。

## <a name="device-context-and-slot-context"></a>设备上下文和槽上下文

设备上下文结构包含指向端点上下文结构的指针的数组。 设备上的每个终结点都有一个终结点上下文结构。 元素1到31点到终结点上下文结构。 元素0指向槽上下文结构，该结构包含设备的上下文信息。

## <a name="command-ring"></a>命令环

软件使用命令循环将命令传递给主机控制器。 其中一些命令定向到主机控制器，某些命令在连接到主机控制器的特定设备上定向。

## <a name="event-ring"></a>事件环

主机控制器使用事件环将事件传递给软件。 也就是说，事件环是宿主控制器用于通知驱动程序操作已完成的结构。

## <a name="doorbell-register-array"></a>Doorbell 寄存器数组

Doorbell 寄存器数组是一组 Doorbell 寄存器，每个连接到该主机控制器的设备一个。 元素1到255是 doorbell 寄存器。 元素0指示命令环中是否有挂起的命令。

软件会通过将上下文信息写入设备的 doorbell 寄存器，通知主机控制器包含与设备相关或与终结点相关的工作。

以下关系图将继续到上图的右侧。 它显示表示单个终结点的其他数据结构。

![usb 3.0 数据结构，显示具有多个包含数据和 tds 的 trbs 的终结点上下文](images/usb3structures02.png)

## <a name="transfer-ring"></a>传输振铃

每个终结点具有一个或多个传输环。 传输环是 (TRBs) 的传输请求块的数组。 每个 TRB 都指向一个连续数据块 (多达 64 KB) ，将作为一个单元在硬件和内存之间传输。

当 USB 3.0 核心堆栈接收到来自 USB 客户端驱动程序的传输请求时，它将标识传输的终结点上下文，然后将传输请求中断到 (TDs) 的一个或多个传输描述符中。 每个 TD 都包含一个或多个 TRBs。

## <a name="endpoint-context"></a>终结点上下文

终结点上下文结构保存单个终结点的上下文信息。 它还具有取消 **排队** 和 **排队** 的成员，这些成员用于跟踪硬件使用 TRBs 的位置以及软件添加 TRBs 的位置。

## <a name="related-topics"></a>相关主题

[Windows 8 中的 USB 调试创新](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P)
