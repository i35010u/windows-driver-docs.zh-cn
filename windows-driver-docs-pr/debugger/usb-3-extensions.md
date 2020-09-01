---
title: USB 3.0 扩展
description: 本部分介绍了 USB 3.0 调试程序扩展命令。
ms.assetid: 7CE2B9F8-50EF-41C0-B306-B7B7A6DA1636
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8a7c344a314fdb35bdbb57b83f9bc69392204eb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215692"
---
# <a name="usb-30-extensions"></a>USB 3.0 扩展

本部分介绍了 USB 3.0 调试程序扩展命令。 这些命令显示 USB 3.0 堆栈中由三个驱动程序维护的数据结构中的信息： USB 3.0 集线器驱动程序、USB 主机控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序。 有关这三个驱动程序的详细信息，请参阅 [Windows 中的 USB 主机端驱动程序](../usbcon/usb-3-0-driver-stack-architecture.md)。 有关 USB 3.0 堆栈中的驱动程序所使用的数据结构的说明，请参阅 [usb 3.0 数据结构](usb-3-0-data-structures.md) 和 [Windows 8 视频中 usb 调试创新](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P) 的第2部分。

USB 3.0 调试程序扩展命令在 Usb3kd.dll 中实现。 若要加载 Usb3kd 命令，请输入调试程序中的 **load usb3kd.dll** 。

## <a name="span-idusb-3-treespan-usb-30-tree"></a><span id="usb-3-tree"></span> USB 3.0 树

USB 3.0 树包含所有 USB 3.0 主机控制器以及连接到 USB 3.0 主机控制器的所有集线器和设备。 下图显示了一个 USB 3.0 树的示例。

![usb 3.0 树显示混合了 usb 3.0 和 usb 2.0 设备根和控制器](images/usb3tree01.png)

图中所示的树有两个 USB 3.0 主机控制器。 请注意，图中所示的每个设备并不是 USB 3.0 设备。 但 (包括集线器) 所示的所有设备都是 USB 3.0 树的一部分，因为每个设备都在源自 USB 3.0 主机控制器的分支上。

可以将该关系图视为两个树，每个树对应一个主机控制器。 但是，当我们使用术语 " *usb 3.0" 树*时，我们将引用所有 USB 3.0 主机控制器及其连接的集线器和设备的集合。

## <a name="getting-started-with-usb-30-debugging"></a>USB 3.0 调试入门

若要开始调试 USB 3.0 问题，请输入 [**！ usb \_ tree**](-usb3kd-usb-tree.md) 命令。 **！ Usb \_ tree**命令显示可用于调查主机控制器、集线器、端口、设备、终结点和 usb 3.0 树的其他元素的命令和地址列表。

## <a name="hub-commands"></a>中心命令

以下扩展命令显示有关 USB 3.0 集线器、设备和端口的信息。 显示的信息取决于 USB 3.0 集线器驱动程序所维护的数据结构。

-   [**！ usb3kd \_ 树**](-usb3kd-usb-tree.md)
-   [**！ usb3kd \_ 信息**](-usb3kd-hub-info.md)
-   [**！ usb3kd \_ \_ fdo 中的信息 \_**](-usb3kd-hub-info-from-fdo.md)
-   [**！ usb3kd \_ 信息**](-usb3kd-device-info.md)
-   [**！ usb3kd \_ \_ 来自 pdo 的设备 \_ 信息**](-usb3kd-device-info-from-pdo.md)
-   [**！ usb3kd \_ 信息**](-usb3kd-port-info.md)

## <a name="ucx-commands"></a>UCX 命令


以下扩展命令显示有关 USB 3.0 主机控制器、设备和端口的信息。 显示的信息基于 USB 主机控制器扩展驱动程序所维护的数据结构。

-   [**！ usb3kd ucx \_ 控制器 \_ 列表**](-usb3kd-ucx-controller-list.md)
-   [**！ usb3kd ucx \_ 控制器**](-usb3kd-ucx-controller.md)
-   [**！ usb3kd ucx \_ 设备**](-usb3kd-ucx-device.md)
-   [**！ usb3kd ucx \_ 终结点**](-usb3kd-ucx-endpoint.md)

## <a name="host-controller-commands"></a>主机控制器命令


以下扩展命令显示 USB 3.0 主机控制器驱动程序所维护的数据结构的信息。

-   [**！ usb3kd. xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)
-   [**！ usb3kd xhci \_ 功能**](-usb3kd-xhci-capability.md)
-   [**！ usb3kd. xhci \_ commandring**](-usb3kd-xhci-commandring.md)
-   [**！ usb3kd. xhci \_ deviceslots**](-usb3kd-xhci-deviceslots.md)
-   [**！ usb3kd. xhci \_ eventring**](-usb3kd-xhci-eventring.md)
-   [**！ usb3kd xhci \_ 注册**](-usb3kd-xhci-registers.md)
-   [**！ usb3kd. xhci \_ resourceusage**](-usb3kd-xhci-resourceusage.md)
-   [**！ usb3kd. xhci \_ trb**](-usb3kd-xhci-trb.md)
-   [**！ usb3kd xhci 正在 \_ 传输**](-usb3kd-xhci-transferring.md)
-   [**！ usb3kd. xhci \_ findowner**](-usb3kd-xhci-findowner.md)

## <a name="miscellaneous-commands"></a>杂项命令

-   [**!usb3kd.usbdstatus**](-usb3kd-usbdstatus.md)
-   [**!usb3kd.urb**](-usb3kd-urb.md)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[RCDRKD 扩展](rcdrkd-extensions.md)