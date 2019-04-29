---
Description: WpdMultiTransportDriver 示例
title: WpdMultiTransportDriver 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddd9d8ca5db775d0985d161f15056c007c2fa5b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370530"
---
# <a name="the-wpdmultitransportdriver-sample"></a>WpdMultiTransportDriver 示例


WPD 驱动程序文档的此部分介绍一个示例 multitransport 驱动程序，WpdMultiTransportDriver，包括在 Windows 驱动程序工具包。

传输已对其便携式设备与计算机进行通信的协议。 示例的传输包括 Internet 协议 (IP)、 蓝牙和 USB。

多个可移植的设备现在支持多个传输协议。 例如，某些单元格手机支持蓝牙和 USB。

Windows 7 之前的版本，如果用户连接的便携式设备，支持多个传输到他们的计算机，Windows 设备管理器将显示有关每个传输 – 唯一节点。 这可能无法表示多个设备已安装。 若要解决此问题，Windows 7 支持 multitransport 驱动程序模型。 此模型可确保只有一个节点将显示为每个 multitransport 支持的设备。

在下图中所示 multitransport 驱动程序堆栈：

![驱动程序堆栈](images/multi_trans_driver_stack.png)

在上一图中，假设 WPD 应用程序 (*App.exe*) 可以启用与 multitransport 和 USB 或蓝牙连接的手机之间来回移动数据。 WPD 复合驱动程序 (*Wpdcomp.dll*) 由 Microsoft 提供，并且包含在 Windows 7。 Multitransport 驱动程序 (*WpdMultiTranscell.dll*) 是假设的供应商提供的驱动程序。

上图描述了通过蓝牙和 USB 的同时连接。 某些驱动程序 mightimplement 此功能。 WpdMultiTransportDriver 支持在任意给定时间一次 （而不是同时） 连接的时间。

此示例驱动程序基于 WDK 中包含 WpdHelloWorldDriver。 查看此部分中的主题之前，先熟悉[WpdHelloWorldDriver](the-sample-driver-architecture.md)。

下表中标识为 WpdHelloWorldDriver 和 WpdMultiTransportDriver 之间的主要差异。

| 修订或更改     | 描述                                                                                                                                                                                                                   |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设备到达时         | 新 multitransport 驱动程序创建给定设备功能唯一标识符 (FUID)、 启用 multitransport 选项、 设置必要的插 (PnP) 值，并设置当前流传输的带宽。 |
| 多个队列支持 | 新 multitransport 驱动程序支持两个 I/O 队列。 （WpdHelloWorldDriver 支持单个队列。）                                                                                                                     |

 

若要探索 multitransport 驱动程序的功能并测试实际传输切换，您可以安装[媒体传输的协议移植工具包](https://www.microsoft.com/download/details.aspx?id=19153)，并使用 MTP 模拟器 (*MtpSimUi.exe)* 应用程序。 通过使用此应用程序，可以安装 Microsoft 的 MTP 驱动程序、 连接或断开与仿真设备的连接和切换传输。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





