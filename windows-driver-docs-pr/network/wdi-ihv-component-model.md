---
title: WDI IHV 组件模型
description: 本部分概述了 WDI 微型端口驱动程序和这些接口的期望的 NDIS 接口。WDI 模型中的 IHV 组件是 NDIS 微型端口。
ms.assetid: FF670015-BB70-4703-BBA9-69130213D7D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e811ce1820fc76c6626b271d31a213b1e0abc0d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387214"
---
# <a name="wdi-ihv-component-model"></a>WDI IHV 组件模型


本部分概述了 WDI 微型端口驱动程序和这些接口的期望的 NDIS 接口。

WDI 模型中的 IHV 组件是 NDIS 微型端口。 它可以与操作系统和其网络堆栈使用现有的和新的 NDIS Api 接口。 Microsoft WLAN 组件位于 WDI IHV 微型端口驱动程序和操作系统的其余部分之间。 它提供了 WDI 接口和现有的 NDIS/本机 WLAN 接口之间的映射。 WDI 命令已打包到作为新的 NDIS Oid 和 WDI 指示打包为新的 NDIS 迹象。 通过进行交互的数据路径[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构使用新的处理程序。

下图显示了整体的体系结构布局和示例的消息流 （即插即用的操作、 Oid 和发送） 从操作系统到旧的本机 WLAN 模型和新 WDI WLAN 模型 IHV 微型端口驱动程序。

![本机 wi-fi 和 wdi 驱动程序比较](images/wdi-model-comparison.png)

除了提供本机 Wi-fi 接口要求的帮助，Microsoft WLAN 组件还可以处理大多数常见的 NDIS 要求。 例如，它处理[ *MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause) NDIS 和需求转换到 WDI 数据和控制路径消息以确保满足 NDIS 要求。 但是，它还提供 IHV 微型端口驱动程序能够执行其他工作。 该驱动程序可以注册在接收通知*MiniportPause*调用以执行任何其他清理操作它想要执行操作期间*MiniportPause*。

 

 





