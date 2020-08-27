---
description: WpdMultiTransportDriver 示例
title: WpdMultiTransportDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f359cd009fd42be801746a9395aca33215238bcf
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969270"
---
# <a name="the-wpdmultitransportdriver-sample"></a>WpdMultiTransportDriver 示例


WPD 驱动程序文档中的此部分介绍了 Windows 驱动程序工具包中包含的 multitransport 驱动程序 WpdMultiTransportDriver 示例。

传输是便携式设备与计算机进行通信时使用的协议。 示例传输包括 Internet 协议 (IP) 、蓝牙和 USB。

许多便携设备现在支持多个传输。 例如，某些手机支持蓝牙和 USB。

在 Windows 7 之前，如果用户将支持多个传输的便携式设备连接到其计算机，则 Windows 设备管理器会为每个传输显示一个唯一的节点–。 这可能意味着已安装多个设备。 若要解决此问题，Windows 7 支持 multitransport 驱动程序模型。 此模型可确保每个支持 multitransport 的设备只显示一个节点。

下图显示了 multitransport 驱动程序堆栈：

![驱动程序堆栈](images/multi_trans_driver_stack.png)

在上图中，假设的 WPD 应用程序 (*App.exe*) 可以在通过 multitransport 启用的手机与 USB 或蓝牙连接之间来回移动数据。 WPD 复合驱动 (*Wpdcomp.dll*) 由 Microsoft 提供，并包含在 Windows 7 中。 Multitransport 驱动程序 (*WpdMultiTranscell.dll*) 是一个假设供应商提供的驱动程序。

上图描述了通过蓝牙和 USB 进行的同时连接。 某些驱动程序 mightimplement 此功能。 WpdMultiTransportDriver 支持单个 (，而不支持在任意给定时间点同时) 连接。

此示例驱动程序基于包含在 WDK 中的 WpdHelloWorldDriver。 查看本部分中的主题之前，请先熟悉 [WpdHelloWorldDriver](the-sample-driver-architecture.md)。

下表中标识了 WpdHelloWorldDriver 与 WpdMultiTransportDriver 之间的主要区别。

| 修订或更改     | 说明                                                                                                                                                                                                                   |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设备到达         | 新的 multitransport 驱动程序 (FUID) 为给定设备创建功能唯一标识符，启用 multitransport 选项，将必要的即插即用设置 (PnP) 值，并设置当前传输带宽。 |
| 多队列支持 | 新的 multitransport 驱动程序支持两个 i/o 队列。  (WpdHelloWorldDriver 支持单个队列。 )                                                                                                                      |

 

若要浏览 multitransport 驱动程序的功能并测试实际传输切换，可以安装 [媒体传输协议移植工具包](https://www.microsoft.com/download/details.aspx?id=19153) ，并使用 MTP 模拟器 (*MtpSimUi.exe) * 应用程序。 通过使用此应用程序，你可以安装 Microsoft 的 MTP 驱动程序、连接或断开与仿真设备的连接，以及交换机传输。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





