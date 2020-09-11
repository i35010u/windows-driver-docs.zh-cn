---
description: 本部分介绍了用于宿主驱动程序开发的高级概念和任务。
title: 'USB 主机控制器扩展 (UCX 的体系结构) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01f8e92419753b000c7ca16ba4371e1fd4a181ec
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010337"
---
# <a name="architecture-usb-host-controller-extension-ucx"></a>体系结构：USB 主控制器扩展 (UCX)


本部分介绍了用于宿主驱动程序开发的高级概念和任务。 如果你正在编写与 Microsoft 提供的 USB 主机控制器扩展驱动程序 ( # A0) 通信的新主机控制器驱动程序，则此部分适用于你。

下面是 [Windows 中 USB 主机端驱动程序](usb-3-0-driver-stack-architecture.md)中显示的图表的修改版本。 此版本隐藏与主机控制器驱动程序开发无关的 USB 客户端驱动程序层的详细信息。

![ucx 体系结构](images/ucx.png)

在上图中，

-   **USB 集线器驱动程序 ( # A0) ** 是 KMDF 驱动程序。 集线器驱动程序负责管理 USB 集线器及其端口、枚举和创建物理设备对象 (PDOs) USB 设备以及其他可能附加到下游端口的集线器。
-   **USB 主机控制器扩展 ( # A0) ** 是堆栈中上面的集线器驱动程序的抽象层，并提供将请求排队到基础主机控制器驱动程序的通用机制。
-   **USB 主机控制器驱动程序** 管理硬件。 Usbxhci.sys 是 Microsoft 提供的一个此类驱动程序，特别是针对 xHCI 规范兼容 USB 控制器硬件。 独立硬件开发人员可能需要编写自己的主机控制器驱动程序，而不是使用收件箱 Usbxhci.sys。 例如，对于不完全符合规范的 XHCI 硬件，因此不能使用 Usbxhci.sys 或用于非 XHCI 硬件，例如 USB over TCP 连接。

使用 [USB 主机控制器扩展 (UCX) 编程接口](/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))，在 UCX 与主机控制器驱动程序之间进行双向通信。 在编译驱动程序时，每个驱动程序都静态链接到 Microsoft 提供的存根库 (Ucx01000) 中的入口点。

下面是为主机控制器驱动程序加载的设备堆栈：

![ucx 设备堆栈](images/ucx-device-stack.png)

## <a name="related-topics"></a>相关主题
[ (USB) 驱动程序的通用串行总线](../index.yml)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)