---
title: WDI 数据路径体系结构
description: 为了与现有的 WLAN 目标设备进行互操作，当前版本的驱动程序接口未指定用于 TX/RX (HCI) 的主机控制器接口。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 550f24f13cf533c4ec009375d026af9df43eca50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840599"
---
# <a name="wdi-datapath-architecture"></a>WDI 数据路径体系结构


为了与现有的 WLAN 目标设备进行互操作，当前版本的驱动程序接口未指定用于 TX/RX (HCI) 的主机控制器接口。 相反，它指定 WDI 和目标适配层之间的请求/指示软件接口， (TAL) 。

WDI 组件实现 NDIS 数据路径接口和主机执行的目标不可知的 TX/RX 函数。 它还维护各个虚拟 WLAN 设备的状态， (端口) 和对等互连状态。

TAL 提供了 TX/RX WLAN 函数，实现依赖于主机控制器接口，还提供控制器和总线接口功能。

![wdi 数据路径框图](images/wdi-datapath-block-diagram.png)

除了 TX/RX 函数外，TAL 还提供了一个 (等到) 的目标接口层，由控件和数据路径使用。 下表列出了等到的责任。

| 等到函数                            | 描述                                                                                                                                                                      |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 管理 Host-Target 通信 | 示例：分配和管理控制和数据路径所需的 DMA 通道。                                                                                               |
| 总线适配/抽象              | 提供标准主机/目标通信 API，以抽象不同总线类型、软件/硬件总线终结点和总线 DMA 引擎之间的通信差异。 |

 

 

 





