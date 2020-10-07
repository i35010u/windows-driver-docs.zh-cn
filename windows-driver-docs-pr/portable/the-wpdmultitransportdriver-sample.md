---
description: WpdMultiTransportDriver 示例
title: WpdMultiTransportDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63cfb0546bfe54bfb378a5f5c05b99f987c20884
ms.sourcegitcommit: 9b3dec2f2cd9a7ed9b340b4794ce6ff4134d8ebe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91787629"
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

| 修订或更改 | 说明 |
|--|--|
| 设备到达 | 新的 multitransport 驱动程序 (FUID) 为给定设备创建功能唯一标识符，启用 multitransport 选项，将必要的即插即用设置 (PnP) 值，并设置当前传输带宽。 |
| 多队列支持 | 新的 multitransport 驱动程序支持两个 i/o 队列。  (WpdHelloWorldDriver 支持单个队列。 )  |

## <a name="related-topics"></a>相关主题

[WPD 驱动程序示例](the-wpd-driver-samples.md)

[MTP 安装程序信息 (.inf) 文件](the-mtp-setup-information---inf--file.md)
