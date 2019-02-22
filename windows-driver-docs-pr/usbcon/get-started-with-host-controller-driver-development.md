---
Description: This section introduces you to high-level concepts and tasks for host driver development.
title: USB 主机控制器扩展 (UCX) 的体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d53d333bc749b6a99394d55ec9adac3eed17d617
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547755"
---
# <a name="architecture-usb-host-controller-extension-ucx"></a>体系结构：USB 主机控制器扩展 (UCX)


本部分介绍高级概念和任务的主机驱动程序开发。 如果你正在编写新的主机与 Microsoft 提供的 USB 主控制器扩展驱动程序 (Ucx01000.sys) 控制器驱动程序进行通信，部分适用于您。

下面是修改后的版本的关系图中所示[USB 宿主端驱动程序在 Windows 中的](usb-3-0-driver-stack-architecture.md)。 此版本将隐藏 USB 客户端驱动程序层，这不是与主机控制器驱动程序开发相关的详细的信息。

![ucx 体系结构](images/ucx.png)

在上图中，

-   **USB 集线器驱动程序 (Usbhub3.sys)** 是 KMDF 驱动程序。 中心驱动程序负责管理 USB 集线器和它们的端口、 枚举和创建的 USB 设备和其他中心的物理设备对象 (PDOs) 可能会连接到其下游的端口。
-   **USB 主机控制器扩展 (Ucx01000.sys)** 是到上面的中心驱动程序堆栈中的抽象层，并提供对基础主机控制器驱动程序的排队请求的通用机制。
-   **USB 主控制器驱动程序**管理硬件。 Usbxhci.sys 是由 Microsoft，该目标 xHCI 规范兼容 USB 控制器的硬件，特别是提供一个此类驱动程序。 可能有必要为独立硬件开发人员能够编写它们自己的主机控制器的驱动程序，而不使用收件箱 Usbxhci.sys。 例如，对于不是完全符合规范，因此不能使用 Usbxhci.sys XHCI 硬件或非 XHCI 硬件，如 USB 通过 TCP 连接。

通过使用采用控制器驱动程序的 UCX 与主机之间的双向通信进行[USB 主机控制器扩展 (UCX) 编程接口](https://msdn.microsoft.com/library/windows/hardware/mt188009)。 编译该驱动程序时，每个驱动程序静态链接到由 Microsoft 提供存根 （stub） 库 (Ucx01000.lib) 中的入口点。

下面是为主机控制器驱动程序加载的设备堆栈：

![ucx 设备堆栈](images/ucx-device-stack.png)

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB) 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



