---
title: USB 2.0 扩展
description: 本部分介绍了 USB 2.0 调试程序扩展命令。 这些命令显示由 USB 2.0 驱动程序堆栈中的驱动程序所维护的数据结构的信息。
ms.assetid: 42A78738-CE0D-42EA-9E3D-04CDC2060266
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 491f61ab730ec76033d021eb228100fe41f3db0d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215718"
---
# <a name="usb-20-extensions"></a>USB 2.0 扩展

本部分介绍了 USB 2.0 调试程序扩展命令。 这些命令显示由 USB 2.0 驱动程序堆栈中的驱动程序所维护的数据结构的信息。 有关这三个驱动程序的详细信息，请参阅 [Windows 中的 USB 主机端驱动程序](../usbcon/usb-3-0-driver-stack-architecture.md)。

USB 2.0 调试程序扩展命令在 Usbkd.dll 中实现。 若要加载 Usbkd 命令，请输入调试程序中的 **load usbkd.dll** 。

## <a name="span-idusb-2-treespan-usb-20-tree"></a><span id="usb-2-tree"></span> USB 2.0 树

USB 2.0 树包含代表 EHCI 主机控制器设备上执行单元的设备节点，以及表示集线器和连接设备的子节点。 此图显示了一个 USB 2.0 树的示例。

![显示 usb 2tree 的图示](images/usbkd01.png)

此关系图显示了一个具有两个执行单元的物理主机控制器设备。 每个执行单元在即插即用设备树中显示为一个设备节点。 一个执行单元显示为 UHCI USB 主机控制器节点，另一个执行单元显示为 EHCI USB 主机控制器节点。 其中每个节点都有一个表示 USB 根集线器的子节点。 每个根集线器都有一个表示连接的 USB 设备的子节点。

请注意，该关系图不是所有节点都从单个父节点中派生出的树。 但是，当我们使用术语 " *USB 2.0 树*" 时，我们将引用一组设备节点，这些节点代表 EHCI 主机控制器设备上的执行单元以及集线器和连接设备的节点。

## <a name="getting-started-with-usb-20-debugging"></a>USB 2.0 调试入门


若要开始调试 USB 2.0 问题，请输入 [**！ usb2tree**](-usbkd-usb2tree.md) 命令。 **！ Usb2tree**命令显示可用于调查主机控制器、集线器、端口、设备、终结点和 USB 2.0 树的其他元素的命令和地址列表。

## <a name="in-this-section"></a>本节内容


-   [**!usbkd.usbhelp**](-usbkd-usbhelp.md)
-   [**！ usbkd。 \_ehcidd**](-usbkd--ehcidd.md)
-   [**！ usbkd。 \_ehciep**](-usbkd--ehciep.md)
-   [**！ usbkd。 \_ehciframe**](-usbkd--ehciframe.md)
-   [**！ usbkd。 \_ehciqh**](-usbkd--ehciqh.md)
-   [**！ usbkd。 \_ehciregs**](-usbkd--ehciregs.md)
-   [**！ usbkd。 \_ehcisitd**](-usbkd--ehcisitd.md)
-   [**！ usbkd。 \_ehcistq**](-usbkd--ehcistq.md)
-   [**！ usbkd。 \_ehcitd**](-usbkd--ehcitd.md)
-   [**！ usbkd。 \_ehcitfer**](-usbkd--ehcitfer.md)
-   [**！ usbkd。 \_ehciitd**](-usbkd--ehciitd.md)
-   [**!usbkd.doesdumphaveusbdata**](-usbkd-doesdumphaveusbdata.md)
-   [**!usbkd.isthisdumpasyncissue**](-usbkd-isthisdumpasyncissue.md)
-   [**!usbkd.urbfunc**](-usbkd-urbfunc.md)
-   [**!usbkd.usb2**](-usbkd-usb2.md)
-   [**!usbkd.usb2tree**](-usbkd-usb2tree.md)
-   [**!usbkd.usbchain**](-usbkd-usbchain.md)
-   [**!usbkd.usbdevobj**](-usbkd-usbdevobj.md)
-   [**!usbkd.usbdpc**](-usbkd-usbdpc.md)
-   [**！ usbkd \_ \_ fdo 中的信息 \_**](-usbkd-ehci-info-from-fdo.md)
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
-   [**！ usbkd hub2 \_ info \_ from \_ fdo**](-usbkd-hub2-info-from-fdo.md)
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

## <a name="related-topics"></a>相关主题

[USB 3.0 扩展](usb-3-extensions.md)

[RCDRKD 扩展](rcdrkd-extensions.md)