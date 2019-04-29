---
title: USB 2.0 扩展
description: 本部分介绍 USB 2.0 调试器扩展命令。 这些命令显示通过 USB 2.0 驱动程序堆栈中的驱动程序维护的数据结构中的信息。
ms.assetid: 42A78738-CE0D-42EA-9E3D-04CDC2060266
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b506fe76da4e30b53a5c220b3b2d0e5a85caafa2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367991"
---
# <a name="usb-20-extensions"></a>USB 2.0 扩展


本部分介绍 USB 2.0 调试器扩展命令。 这些命令显示通过 USB 2.0 驱动程序堆栈中的驱动程序维护的数据结构中的信息。 有关上述三个的驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkId=251983)。

USB 2.0 调试器扩展命令中 Usbkd.dll 实现。 若要加载的 Usbkd 命令，请输入 **.load usbkd.dll**在调试器中。

## <a name="span-idusb-2-treespanspan-idusb2treespanusb-20-tree"></a><span id="usb-2-tree"></span><span id="USB_2_TREE"></span>USB 2.0 树


USB 2.0 树包含表示 EHCI 以及表示中心的子节点的主机控制器设备和连接的设备上执行单元的设备节点。 此图显示了 USB 2.0 树的示例。

![显示 usb 2tree 的关系图](images/usbkd01.png)

该图显示一个物理主机控制器设备具有两个执行单位。 每个执行单元将显示为插设备树中的设备节点。 一个执行单位显示为 UHCI USB 主机控制器节点，并作为 EHCI USB 主控制器节点显示其他执行单元。 每个这些节点具有表示 USB 根集线器的子节点。 每个根中心都有一个子节点表示连接的 USB 设备。

请注意，在关系图不是内容而言，并非所有节点都源自的单一父节点的树。 但是，我们使用术语*USB 2.0 树*，指使用的设备节点表示的节点的中心以及 EHCI 主机控制器设备和连接的设备上执行单元集。

## <a name="span-idgettingstartedwithusb20debuggingspanspan-idgettingstartedwithusb20debuggingspangetting-started-with-usb-20-debugging"></a><span id="getting_started_with_usb_2.0_debugging"></span><span id="GETTING_STARTED_WITH_USB_2.0_DEBUGGING"></span>开始使用 USB 2.0 调试


若要开始调试一个 USB 2.0 的问题，请输入[ **！ usb2tree** ](-usbkd-usb2tree.md)命令。 **！ Usb2tree**命令显示命令和可用于调查主机控制器、 中心、 端口、 设备、 端点和 USB 2.0 树的其他元素的地址的列表。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [**!usbkd.usbhelp**](-usbkd-usbhelp.md)
-   [**!usbkd.\_ehcidd**](-usbkd--ehcidd.md)
-   [**！ usbkd。\_ehciep**](-usbkd--ehciep.md)
-   [**!usbkd.\_ehciframe**](-usbkd--ehciframe.md)
-   [**!usbkd.\_ehciqh**](-usbkd--ehciqh.md)
-   [**！ usbkd。\_ehciregs**](-usbkd--ehciregs.md)
-   [**!usbkd.\_ehcisitd**](-usbkd--ehcisitd.md)
-   [**!usbkd.\_ehcistq**](-usbkd--ehcistq.md)
-   [**!usbkd.\_ehcitd**](-usbkd--ehcitd.md)
-   [**！ usbkd。\_ehcitfer**](-usbkd--ehcitfer.md)
-   [**!usbkd.\_ehciitd**](-usbkd--ehciitd.md)
-   [**!usbkd.doesdumphaveusbdata**](-usbkd-doesdumphaveusbdata.md)
-   [**!usbkd.isthisdumpasyncissue**](-usbkd-isthisdumpasyncissue.md)
-   [**!usbkd.urbfunc**](-usbkd-urbfunc.md)
-   [**!usbkd.usb2**](-usbkd-usb2.md)
-   [**!usbkd.usb2tree**](-usbkd-usb2tree.md)
-   [**!usbkd.usbchain**](-usbkd-usbchain.md)
-   [**!usbkd.usbdevobj**](-usbkd-usbdevobj.md)
-   [**!usbkd.usbdpc**](-usbkd-usbdpc.md)
-   [**!usbkd.ehci\_info\_from\_fdo**](-usbkd-ehci-info-from-fdo.md)
-   [**!usbkd.usbdevh**](-usbkd-usbdevh.md)
-   [**!usbkd.usbep**](-usbkd-usbep.md)
-   [**!usbkd.usbfaildata**](-usbkd-usbfaildata.md)
-   [**!usbkd.usbhcdext**](-usbkd-usbhcdext.md)
-   [**!usbkd.usbdstatus**](-usbkd-usbdstatus.md)
-   [**!usbkd.usbhcdhccontext**](-usbkd-usbhcdhccontext.md)
-   [**!usbkd.usbhcdlist**](-usbkd-usbhcdlist.md)
-   [**!usbkd.usbhcdlistlogs**](-usbkd-usbhcdlistlogs.md)
-   [**!usbkd.usbhcdlog**](-usbkd-usbhcdlog.md)
-   [**!usbkd.usbhcdlogex**](-usbkd-usbhcdlogex.md)
-   [**!usbkd.usbhcdpnp**](-usbkd-usbhcdpnp.md)
-   [**!usbkd.usbhcdpow**](-usbkd-usbhcdpow.md)
-   [**!usbkd.hub2\_info\_from\_fdo**](-usbkd-hub2-info-from-fdo.md)
-   [**!usbkd.usbhuberr**](-usbkd-usbhuberr.md)
-   [**!usbkd.usbhubext**](-usbkd-usbhubext.md)
-   [**!usbkd.usbhubinfo**](-usbkd-usbhubinfo.md)
-   [**!usbkd.usbhublog**](-usbkd-usbhublog.md)
-   [**!usbkd.usbhubmddevext**](-usbkd-usbhubmddevext.md)
-   [**!usbkd.usbhubmdpd**](-usbkd-usbhubmdpd.md)
-   [**!usbkd.usbhubpd**](-usbkd-usbhubpd.md)
-   [**!usbkd.usbhubs**](-usbkd-usbhubs.md)
-   [**!usbkd.usblist**](-usbkd-usblist.md)
-   [**!usbkd.usbpo**](-usbkd-usbpo.md)
-   [**!usbkd.usbpdos**](-usbkd-usbpdos.md)
-   [**!usbkd.usbpdoxls**](-usbkd-usbpdoxls.md)
-   [**!usbkd.usbpnp**](-usbkd-usbpnp.md)
-   [**!usbkd.usbportisasyncadv**](-usbkd-usbportisasyncadv.md)
-   [**!usbkd.usbportmdportlog**](-usbkd-usbportmdportlog.md)
-   [**!usbkd.usbportmddcontext**](-usbkd-usbportmddcontext.md)
-   [**!usbkd.usbportmddevext**](-usbkd-usbportmddevext.md)
-   [**!usbkd.usbtriage**](-usbkd-usbtriage.md)
-   [**!usbkd.usbtt**](-usbkd-usbtt.md)
-   [**!usbkd.usbtx**](-usbkd-usbtx.md)
-   [**!usbkd.usbusb2ep**](-usbkd-usbusb2ep.md)
-   [**!usbkd.usbusb2tt**](-usbkd-usbusb2tt.md)
-   [**!usbkd.usbver**](-usbkd-usbver.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[USB 3.0 扩展](usb-3-extensions.md)

[RCDRKD 扩展](rcdrkd-extensions.md)

 

 






