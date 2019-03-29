---
Description: The section describes architecture of USB Device Emulation(UDE) that emulates the behavior of a USB host controller and a connected device.
title: USB 设备仿真 (UDE) 的体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 737b1f29ef5d9006c5f3b70ae090e15d33d88a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568998"
---
# <a name="architecture-usb-device-emulation-ude"></a>体系结构：USB 设备模拟 (UDE)


本节介绍模拟 USB 主控制器的行为的 USB 设备 Emulation(UDE) 和连接的设备的体系结构。 通过使用 UDE，非 USB 硬件可以使用与通信上层[USB 宿主端驱动程序在 Windows 中的](usb-device-side-drivers-in-windows.md)。

## <a name="ude-drivers"></a>UDE 驱动程序


![usb 设备仿真 (ude)](images/ude-arch.png)

在上图中，

-   **USB 集线器驱动程序 (Usbhub3.sys)** 是 KMDF 驱动程序。 中心驱动程序负责管理 USB 集线器和它们的端口、 枚举和创建的 USB 设备和其他中心的物理设备对象 (PDOs) 可能会连接到其下游的端口。
-   **USB 主机控制器扩展 (Ucx01000.sys)** 是到上面的中心驱动程序堆栈中的抽象层，并提供对基础主机控制器驱动程序的排队请求的通用机制。
-   **UDE 类扩展**(UdeCx) 是 UDE 客户端驱动程序通过客户端实现回调函数调用。 类扩展提供的例程创建 UDE 对象并对其进行管理的客户端驱动程序。
-   **UDE 客户端驱动程序**管理与 WDF 和 UDE Api 进行交互的硬件。 上边缘与 WDF 和 UDE 类扩展使用的 USB 构造进行通信。 其下边缘与使用的硬件接口的硬件进行通信。
-   自定义硬件要求：例如，可以模拟 PCI 硬件作为 USB 设备进行处理。

## <a name="ude-device-nodes"></a>UDE 设备节点


下面是为 UDE 客户端驱动程序加载的设备堆栈：

![usb 设备仿真 (ude) 设备节点](images/ude-dev-nodes.png)

 

 




