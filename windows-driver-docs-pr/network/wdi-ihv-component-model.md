---
title: WDI IHV 组件模型
description: 本部分概述了 WDI 微型端口驱动程序的 NDIS 接口以及这些接口的预期。WDI 模型中的 IHV 组件是一个 NDIS 小型端口。
ms.assetid: FF670015-BB70-4703-BBA9-69130213D7D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14e74013b8868a8014ba621d492051e7a37e5d7b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216520"
---
# <a name="wdi-ihv-component-model"></a>WDI IHV 组件模型


本部分概述了 WDI 微型端口驱动程序的 NDIS 接口以及这些接口的预期。

WDI 模型中的 IHV 组件是一个 NDIS 小型端口。 它使用现有的和新的 NDIS Api 与操作系统及其网络堆栈建立接口。 Microsoft WLAN 组件位于 WDI IHV 微型端口驱动程序与操作系统的其余部分之间。 它提供 WDI 接口与现有 NDIS/Native WLAN 接口之间的映射。 WDI 命令封装为新的 NDIS Oid，WDI 指示打包为新的 NDIS 指示。 数据路径使用新的处理程序通过 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构进行交互。

下图显示了完整的体系结构布局和消息 (PNP 操作、Oid 和消息的示例流，并将) 从操作系统发送到旧的本机 WLAN 模型和新的 WDI WLAN 模型的 IHV 微型端口驱动程序。

![本机 wi-fi 和 wdi 驱动程序比较](images/wdi-model-comparison.png)

除了帮助提供本机 Wi-fi 接口要求以外，Microsoft WLAN 组件还处理大多数常见的 NDIS 要求。 例如，它从 NDIS 处理 [*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause) 要求，并将其转换为 WDI 数据和控制路径消息，以确保满足 NDIS 要求。 不过，它还为 IHV 微型端口驱动程序提供了执行其他工作的能力。 该驱动程序可以注册，以在 *MiniportPause* 调用时收到通知，以便在 *MiniportPause*期间执行任何其他清理操作。

 

