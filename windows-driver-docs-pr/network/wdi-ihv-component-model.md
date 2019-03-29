---
title: WDI IHV 组件模型
description: 本部分概述了 WDI 微型端口驱动程序和这些接口的期望的 NDIS 接口。WDI 模型中的 IHV 组件是 NDIS 微型端口。
ms.assetid: FF670015-BB70-4703-BBA9-69130213D7D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d7a7f698be54a2cfcc85a03cf1bea92ab34d01a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568071"
---
# <a name="wdi-ihv-component-model"></a>WDI IHV 组件模型


本部分概述了 WDI 微型端口驱动程序和这些接口的期望的 NDIS 接口。

WDI 模型中的 IHV 组件是 NDIS 微型端口。 它可以与操作系统和其网络堆栈使用现有的和新的 NDIS Api 接口。 Microsoft WLAN 组件位于 WDI IHV 微型端口驱动程序和操作系统的其余部分之间。 它提供了 WDI 接口和现有的 NDIS/本机 WLAN 接口之间的映射。 WDI 命令已打包到作为新的 NDIS Oid 和 WDI 指示打包为新的 NDIS 迹象。 通过进行交互的数据路径[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构使用新的处理程序。

下图显示了整体的体系结构布局和示例的消息流 （即插即用的操作、 Oid 和发送） 从操作系统到旧的本机 WLAN 模型和新 WDI WLAN 模型 IHV 微型端口驱动程序。

![本机 wi-fi 和 wdi 驱动程序比较](images/wdi-model-comparison.png)

除了提供本机 Wi-fi 接口要求的帮助，Microsoft WLAN 组件还可以处理大多数常见的 NDIS 要求。 例如，它处理[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418) NDIS 和需求转换到 WDI 数据和控制路径消息以确保满足 NDIS 要求。 但是，它还提供 IHV 微型端口驱动程序能够执行其他工作。 该驱动程序可以注册在接收通知*MiniportPause*调用以执行任何其他清理操作它想要执行操作期间*MiniportPause*。

 

 





