---
title: WDI 数据路径体系结构
description: 若要与现有 WLAN 目标设备进行互操作，驱动程序接口的当前版本不会指定 TX/rx 主机控制器接口 (HCI)。
ms.assetid: 22684939-A8B5-4687-B1BC-B3A27B2540A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d6347f13056b75468b057c92000875b7d4af487
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367531"
---
# <a name="wdi-datapath-architecture"></a>WDI 数据路径体系结构


若要与现有 WLAN 目标设备进行互操作，驱动程序接口的当前版本不会指定 TX/rx 主机控制器接口 (HCI)。 相反，它指定 WDI 和目标适配层 （谈论） 之间的请求/指示软件接口。

WDI 组件实现 NDIS 数据路径接口和主机执行的目标不可知 TX/RX 函数。 它还维护特定于对等方的状态和单个虚拟 WLAN 设备 （端口） 的状态。

谈论提供实现依赖于主机控制器接口，TX/RX WLAN 函数，以及控制器和总线接口函数。

![wdi 数据路径框图](images/wdi-datapath-block-diagram.png)

TX/RX 函数中，除了谈论提供由控制和数据路径目标接口层 (TIL)。 下表中列出的 TIL 职责。

| 磁贴函数                            | 描述                                                                                                                                                                      |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 管理的主机目标的通信 | 例如：分配和管理所需的控制和数据路径的 DMA 通道。                                                                                               |
| 总线适应/抽象              | 提供标准的主机目标通信 API，用于提取其他总线类型、 软件/硬件总线终结点和总线 DMA 引擎之间的通信差异。 |

 

 

 





