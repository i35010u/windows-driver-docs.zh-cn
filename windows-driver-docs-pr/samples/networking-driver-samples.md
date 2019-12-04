---
title: 网络驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义网络驱动程序的起点。
ms.assetid: 97C88E82-96AA-41AD-9B1F-3EB848A08BD8
ms.date: 12/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8384011200e13b5f3a5c308a04d23b78d7475084
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735255"
---
# <a name="networking-driver-samples"></a>网络驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义网络驱动程序的起点。

| 示例 | 描述 |
| --- | --- |
| [Bindview](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/bindview-network-configuration-utility) | 演示如何使用 INetCfg Api 枚举、安装、卸载、绑定和取消绑定网络组件的应用程序。 |
| [Fakemodem](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/fakemodem-driver) | 演示了一个简单的无控制器调制解调器驱动程序。 |
| [Hyper-v 可扩展交换机扩展筛选器](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hyper-v-extensible-switch-extension-filter-driver) | 用于实现 Hyper-v 可扩展交换机扩展筛选器驱动程序的基库。 |
| [NDIS 6.0 筛选器](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-60-filter-driver) | 该示例是一个无需传递 NDIS 6 筛选器驱动程序，它演示了 NDIS 6.0 筛选器驱动程序的基本原则。 |
| [NDIS MUX 中间驱动程序和通知对象](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-mux-intermediate-driver-and-notify-object) | 一种 NDIS 6.0 驱动程序，用于演示 "N：1" MUX 驱动程序的操作。 此示例在一个较低的适配器上创建多个虚拟网络设备。 |
| [无连接 NDIS 6.0 和6.3 协议驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-connection-less-protocol-wdm-driver-sample) | 此驱动程序支持使用 ReadFile/WriteFile 调用从用户模式发送和接收原始以太网帧。 作为 NDIS 协议驱动程序，它说明了如何建立和拆卸到以太网适配器的绑定。 |
| [无连接 NDIS 6.0 协议驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/connection-less-ndis-60-protocol-kmdf-sample-driver)| 此驱动程序支持使用 ReadFile/WriteFile 调用从用户模式发送和接收原始以太网帧。 作为 NDIS 协议驱动程序，它说明了如何建立和拆卸到以太网适配器的绑定。 |
| [NDIS 虚拟微型端口驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ndis-virtual-miniport-driver) | 演示 NDIS 微型端口驱动程序的功能，而无需物理网络适配器。 |
| [OSR USB-FX2 开发板的收音机交换机测试驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/radio-switch-test-driver-for-osr-usb-fx2-development-board) | 演示如何为 OSR USB-FX2 开发板的无线开关构建 HID 驱动程序。 |
| [收音机管理器](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-radio-management-sample) | 演示如何构建收音机管理器以用于 Windows 收音机管理 Api。 |
| [WDI 示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/wdi-samples) | 此示例演示如何使用 WLAN WDI。 |
| [WFP 数据包修改](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-packet-modification-sample) | 演示 Windows 筛选平台（WFP）的数据包修改功能。 |
| [WFP 流量检查](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-traffic-inspection-sample) | 演示 Windows 筛选平台（WFP）的流量检查功能。  |
| [WFP MSN Messenger 监视器](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-msn-messenger-monitor-sample) | 演示 Windows 筛选平台（WFP）的流检查功能的示例应用程序和驱动程序。 |
| [WFP 流编辑](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-stream-edit-sample) | 演示如何使用 Windows 筛选平台（WFP）替换传输控制协议（TCP）连接的字符串模式。 |
| [Windows 筛选平台](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/windows-filtering-platform-sample) | 这是一个示例防火墙。 它有一个命令行接口，可用于在各种情况下在不同的 WFP 层上添加筛选器。 此外，它还公开用于注入、基本操作、代理和流检查的标注。 |
| [本机 Wi-fi IHV 服务](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ihv-sample-ui) | 演示适用于本机 Wi-fi 的 IHV 扩展性。 |
| [WSK TCP Echo 服务器](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/wsk-tcp-echo-server) | 此示例驱动程序是一个最小化的驱动程序，旨在演示如何使用 Winsock 内核（WSK）编程接口。 |
