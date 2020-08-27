---
description: 本部分介绍了模拟 USB 主机控制器和连接的设备的行为的 USB 设备仿真 (UDE) 的体系结构。
title: 'USB 设备仿真 (UDE 的体系结构) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2ff8781eb4f27dfa4016f250825e024352659be
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968930"
---
# <a name="architecture-usb-device-emulation-ude"></a>体系结构：USB 设备模拟 (UDE)


本部分介绍了模拟 USB 主机控制器和连接的设备的行为的 USB 设备仿真 (UDE) 的体系结构。 通过使用 UDE，非 USB 硬件可以通过使用 [Windows 中的 USB 主机端驱动程序](usb-device-side-drivers-in-windows.md)与上层通信。

## <a name="ude-drivers"></a>UDE 驱动程序


![usb 设备仿真 (ude) ](images/ude-arch.png)

在上图中，

-   **USB 集线器驱动程序 ( # A0) ** 是 KMDF 驱动程序。 集线器驱动程序负责管理 USB 集线器及其端口、枚举和创建物理设备对象 (PDOs) USB 设备以及其他可能附加到下游端口的集线器。
-   **USB 主机控制器扩展 ( # A0) ** 是堆栈中上面的集线器驱动程序的抽象层，并提供将请求排队到基础主机控制器驱动程序的通用机制。
-   **UDE 类扩展** (UdeCx) 通过客户端实现的回调函数调用 UDE 客户端驱动程序。 类扩展提供用于创建和管理 UDE 对象的客户端驱动程序例程。
-   **UDE 客户端驱动程序** 管理硬件，同时与 WDF 和 UDE api 交互。 上边缘使用 USB 构造与 WDF 和 UDE 类扩展通信。 它的下边缘使用硬件接口与硬件通信。
-   自定义硬件：例如，PCI 硬件可以模拟为作为 USB 设备使用。

## <a name="ude-device-nodes"></a>UDE 设备节点


以下是为 UDE 客户端驱动程序加载的设备堆栈：

![usb 设备仿真 (ude) 设备节点](images/ude-dev-nodes.png)

 

 




