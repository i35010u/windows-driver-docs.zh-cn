---
title: 调度 IRQL 跟踪
description: 调度 IRQL 跟踪
keywords:
- 调度级别标志 WDK 网络
- IRQLs WDK 网络
- 网络驱动程序 WDK，IRQLs
- 当前 IRQLs WDK 网络
- 调度 IRQL 跟踪 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f4933e3aa4a57c245fe5542d2227458255c092
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789781"
---
# <a name="dispatch-irql-tracking"></a>调度 IRQL 跟踪





为了提高系统性能，某些 NDIS 函数 (例如， [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数) 包括指示当前 IRQL 的调度级别标志。 正确使用调度级别标志可帮助避免不必要的设置 IRQL 的尝试。

还有其他一些标志来控制其他属性，但派单级别标志的名称为：

NDIS \_ 发送 \_ 标志 \_ 调度 \_ 级别

NDIS \_ 发送 \_ 完成 \_ 标志 \_ 调度 \_ 级别

NDIS \_ 接收 \_ 标志 \_ 调度 \_ 级别

NDIS \_ 返回 \_ 标志 \_ 调度 \_ 级别

\_ \_ \_ 调度 \_ 级别的 NDIS RWL

调用方必须从已知的当前 IRQL 确定调度级别标志设置，而不是通过测试 IRQL 来确定。 例如，你知道 IRQL，因为它是驱动程序设计的固定特征，或驱动程序已保存当前的 IRQL。

如果已知的当前 IRQL 为调度 \_ 级别，则调用方应设置此标志。 如果当前的 IRQL 未知，或调用方未在调度 \_ 级别运行，则调用方应清除此标志。 如果调用方为 NDIS，则被调用函数应测试此标志，以避免更改 IRQL。

驱动程序不应测试 IRQL 来确定调度级别标志的值。 测试将违背标志的用途。 如有必要，被调用函数可以简单地执行测试。 驱动程序如何确定应该或不应该将标志设置为留给特定驱动程序的设计。

 

