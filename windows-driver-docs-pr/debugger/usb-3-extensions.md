---
title: USB 3.0 扩展
description: 本部分介绍 USB 3.0 调试器扩展命令。
ms.assetid: 7CE2B9F8-50EF-41C0-B306-B7B7A6DA1636
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f847cd70475a111c3536201b17c8c26111f8a775
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523733"
---
# <a name="usb-30-extensions"></a>USB 3.0 扩展


本部分介绍 USB 3.0 调试器扩展命令。 这些命令将显示由三个 USB 3.0 堆栈中的驱动程序维护的数据结构中的信息： USB 3.0 集线器驱动程序、 USB 主控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序。 有关上述三个的驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkId=251983)。 使用 USB 3.0 堆栈中的驱动程序的数据结构的说明，请参阅[USB 3.0 数据结构](usb-3-0-data-structures.md)和的第 2 部分[USB 调试 Windows 8 中创新](https://go.microsoft.com/fwlink/p/?LinkID=249153)视频。

USB 3.0 调试器扩展命令中 Usb3kd.dll 实现。 若要加载的 Usb3kd 命令，请输入 **.load usb3kd.dll**在调试器中。

## <a name="span-idusb-3-treespanspan-idusb3treespanusb-30-tree"></a><span id="usb-3-tree"></span><span id="USB_3_TREE"></span>USB 3.0 树


USB 3.0 树包含所有 USB 3.0 主机控制器和所有集线器和连接到 USB 3.0 主控制器的设备。 下图显示了 USB 3.0 树的示例。

![usb 3.0 树中显示多个 usb 3.0 和 usb 2.0 设备根和控制器](images/usb3tree01.png)

在关系图中所示的树包含两个 USB 3.0 主控制器。 请注意，在关系图中所示不是每个设备的 USB 3.0 设备。 但所有显示 （包括中心） 的设备都是 USB 3.0 树的一部分，因为每个设备上源自 USB 3.0 主控制器的分支。

您可以为两个树，分别用于每个主机控制器将关系图。 但是，我们使用术语*USB 3.0 树*，指使用的所有 USB 3.0 主机控制器以及它们已连接的中心和设备组。

## <a name="span-idgetting-started-with-usb-30-debuggingspanspan-idgettingstartedwithusb30debuggingspangetting-started-with-usb-30-debugging"></a><span id="getting-started-with-usb-3.0-debugging"></span><span id="GETTING_STARTED_WITH_USB_3.0_DEBUGGING"></span>开始使用 USB 3.0 调试


若要开始调试 USB 3.0 问题，请输入[ **！ usb\_树**](-usb3kd-usb-tree.md)命令。 **！ Usb\_树**命令显示命令和可用于调查主机控制器、 中心、 端口、 设备、 端点和 USB 3.0 树的其他元素的地址的列表。

## <a name="span-idhub-commandsspanspan-idhubcommandsspanspan-idhubcommandsspanhub-commands"></a><span id="hub-commands"></span><span id="hub_commands"></span><span id="HUB_COMMANDS"></span>中心命令


以下扩展命令显示有关 USB 3.0 集线器、 设备和端口信息。 显示的信息基于 USB 3.0 集线器驱动程序维护的数据结构。

-   [**！ usb3kd.usb\_树**](-usb3kd-usb-tree.md)
-   [**!usb3kd.hub\_info**](-usb3kd-hub-info.md)
-   [**!usb3kd.hub\_info\_from\_fdo**](-usb3kd-hub-info-from-fdo.md)
-   [**!usb3kd.device\_info**](-usb3kd-device-info.md)
-   [**!usb3kd.device\_info\_from\_pdo**](-usb3kd-device-info-from-pdo.md)
-   [**!usb3kd.port\_info**](-usb3kd-port-info.md)

## <a name="span-iducxcommandsspanspan-iducxcommandsspanspan-iducxcommandsspanucx-commands"></a><span id="UCX_commands"></span><span id="ucx_commands"></span><span id="UCX_COMMANDS"></span>UCX 命令


以下扩展命令显示有关 USB 3.0 主机控制器、 设备和端口信息。 显示的信息基于 USB 主控制器扩展驱动程序所维护的数据结构。

-   [**!usb3kd.ucx\_controller\_list**](-usb3kd-ucx-controller-list.md)
-   [**!usb3kd.ucx\_controller**](-usb3kd-ucx-controller.md)
-   [**!usb3kd.ucx\_device**](-usb3kd-ucx-device.md)
-   [**!usb3kd.ucx\_endpoint**](-usb3kd-ucx-endpoint.md)

## <a name="span-idhostcontrollercommandsspanspan-idhostcontrollercommandsspanspan-idhostcontrollercommandsspanhost-controller-commands"></a><span id="Host_controller_commands"></span><span id="host_controller_commands"></span><span id="HOST_CONTROLLER_COMMANDS"></span>主机控制器命令


以下扩展命令显示从 USB 3.0 主机控制器驱动程序维护的数据结构的信息。

-   [**!usb3kd.xhci\_dumpall**](-usb3kd-xhci-dumpall.md)
-   [**!usb3kd.xhci\_capability**](-usb3kd-xhci-capability.md)
-   [**!usb3kd.xhci\_commandring**](-usb3kd-xhci-commandring.md)
-   [**!usb3kd.xhci\_deviceslots**](-usb3kd-xhci-deviceslots.md)
-   [**!usb3kd.xhci\_eventring**](-usb3kd-xhci-eventring.md)
-   [**!usb3kd.xhci\_registers**](-usb3kd-xhci-registers.md)
-   [**!usb3kd.xhci\_resourceusage**](-usb3kd-xhci-resourceusage.md)
-   [**!usb3kd.xhci\_trb**](-usb3kd-xhci-trb.md)
-   [**!usb3kd.xhci\_transferring**](-usb3kd-xhci-transferring.md)
-   [**!usb3kd.xhci\_findowner**](-usb3kd-xhci-findowner.md)

## <a name="span-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanmiscellaneous-commands"></a><span id="Miscellaneous_commands"></span><span id="miscellaneous_commands"></span><span id="MISCELLANEOUS_COMMANDS"></span>杂项命令


-   [**!usb3kd.usbdstatus**](-usb3kd-usbdstatus.md)
-   [**!usb3kd.urb**](-usb3kd-urb.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






