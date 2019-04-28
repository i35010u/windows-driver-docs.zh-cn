---
title: 网络驱动程序示例
description: 此目录中的驱动程序示例为编写你的设备的自定义网络驱动程序提供的起始点。
ms.assetid: 97C88E82-96AA-41AD-9B1F-3EB848A08BD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d32596886982c9e1c549b1cf17ca5ffb73ec4a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345955"
---
# <a name="networking-driver-samples"></a>网络驱动程序示例


此目录中的驱动程序示例为编写你的设备的自定义网络驱动程序提供的起始点。

## <a name="networking"></a>网络


| 示例名称                                                | 解决方案                                                                 | 描述                                                                                                                                                                                                                            |
|------------------------------------------------------------|--------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Bindview                                                   | [bindview](https://go.microsoft.com/fwlink/p/?LinkId=617732)              | 演示如何使用 INetCfg Api 来枚举应用程序安装、 卸载、 绑定和取消绑定网络组件。                                                                                                         |
| Fakemodem                                                  | [fakemodem](https://go.microsoft.com/fwlink/p/?LinkId=617733)             | 演示一个简单的控制器的无调制解调器驱动程序。                                                                                                                                                                                    |
| HYPER-V 可扩展交换机扩展筛选器                 | [扩展插件](https://go.microsoft.com/fwlink/p/?LinkId=617913)            | 用于实现的 HYPER-V 可扩展交换机扩展筛选器驱动程序的基库。                                                                                                                                                  |
| NDIS 6.0 筛选                                            | [filter](https://go.microsoft.com/fwlink/p/?LinkId=617915)                | 该示例是一个无操作传递 NDIS 6 筛选器驱动程序演示 NDIS 6.0 筛选器驱动程序的基本原理。                                                                                                          |
| NDIS MUX 中间层驱动程序并通知对象             | [mux](https://go.microsoft.com/fwlink/p/?LinkId=617916)                   | NDIS 6.0 驱动程序，演示"N:1"MUX 驱动程序的操作。 该示例创建一个较低适配器之上的多个虚拟网络设备。                                                                        |
| 无连接的 NDIS 6.0 和 6.3 协议驱动程序            | [ndisprot60](https://go.microsoft.com/fwlink/p/?LinkId=617917)            | 此驱动程序支持发送和接收原始以太网帧使用 ReadFile/WriteFile 调用从用户模式。 与的 NDIS 协议驱动程序，它演示了如何建立和关闭到以太网适配器的绑定。                 |
| 无连接的 NDIS 6.0 协议驱动程序                    | [ndisprot\_kmdf](https://go.microsoft.com/fwlink/p/?LinkId=620197)        | 此驱动程序支持发送和接收原始以太网帧使用 ReadFile/WriteFile 调用从用户模式。 与的 NDIS 协议驱动程序，它演示了如何建立和关闭到以太网适配器的绑定。                 |
| NDIS 虚拟微型端口驱动程序                               | [netvmini](https://go.microsoft.com/fwlink/p/?LinkId=617918)              | 演示而无需物理网络适配器的 NDIS 微型端口驱动程序的功能。                                                                                                                                |
| OSR USB FX2 开发板的单选交换机测试驱动程序 | [HidSwitchDriverSample](https://go.microsoft.com/fwlink/p/?LinkId=617919) | 演示如何构建为 OSR USB FX2 开发板的无线开关的 HID 驱动程序。                                                                                                                                   |
| 单选管理器                                              | [RadioManagerSample](https://go.microsoft.com/fwlink/p/?LinkId=617920)    | 演示如何构建一个单选管理器用于与 Windows 单选管理 Api。                                                                                                                                          |
| WFP 数据包修改                                    | [ddproxy](https://go.microsoft.com/fwlink/p/?LinkId=617930)               | 演示数据包修改功能的 Windows 筛选平台 (WFP)。                                                                                                                                             |
| WFP 通信检查                                     | [inspect](https://go.microsoft.com/fwlink/p/?LinkId=617931)               | 演示流量检查功能的 Windows 筛选平台 (WFP)。                                                                                                                                              |
| WFP MSN Messenger 监视器                                  | [msnmntr](https://go.microsoft.com/fwlink/p/?LinkId=617932)               | 示例应用程序和驱动程序演示流检查功能的 Windows 筛选平台 (WFP)。                                                                                                              |
| WFP Stream 编辑                                            | [stmedit](https://go.microsoft.com/fwlink/p/?LinkId=617933)               | 演示如何替换为使用 Windows 筛选平台 (WFP) 的传输控制协议 (TCP) 连接的字符串模式。                                                                                               |
| Windows 筛选平台                                 | [WFPSampler](https://go.microsoft.com/fwlink/p/?LinkId=620198)            | 这是一个示例防火墙。 它具有一个命令行接口，允许在各种条件下的各 WFP 层添加筛选器。 此外，它公开注入、 基本操作，设置代理，和流检查标注。 |
| 本机 Wi-fi IHV 服务                                   | [wlan](https://go.microsoft.com/fwlink/p/?LinkId=617934)                  | 演示用于本机 Wi-fi IHV 可扩展性。                                                                                                                                                                                       |
| WSK TCP Echo 服务器                                        | [echosrv](https://go.microsoft.com/fwlink/p/?LinkId=617935)               | 此示例驱动程序是一个最小的驱动程序，用于演示的 Winsock Kernel (WSK) 编程接口的使用情况。                                                                                                               |

 

 

 




