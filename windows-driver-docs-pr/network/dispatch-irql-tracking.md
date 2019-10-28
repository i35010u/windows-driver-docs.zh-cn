---
title: 调度 IRQL 跟踪
description: 调度 IRQL 跟踪
ms.assetid: ac559f4f-0138-4b9a-8f1b-44a2973fd6a1
keywords:
- 调度级别标志 WDK 网络
- IRQLs WDK 网络
- 网络驱动程序 WDK，IRQLs
- 当前 IRQLs WDK 网络
- 调度 IRQL 跟踪 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b9b0184b3d69aafadc064ba3fb7666309f42fdf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838138"
---
# <a name="dispatch-irql-tracking"></a>调度 IRQL 跟踪





为了提高系统性能，某些 NDIS 函数（例如， [*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数）包含用于指示当前 IRQL 的调度级别标志。 正确使用调度级别标志可帮助避免不必要的设置 IRQL 的尝试。

还有其他一些标志来控制其他属性，但派单级别标志的名称为：

NDIS\_\_调度\_级别发送\_标志

NDIS\_发送\_完整\_标志\_调度\_级别

NDIS\_接收\_标志\_调度\_级别

NDIS\_返回\_标志\_调度\_级别

\_调度\_级别，NDIS\_RWL\_

调用方必须从已知的当前 IRQL 确定调度级别标志设置，而不是通过测试 IRQL 来确定。 例如，你知道 IRQL，因为它是驱动程序设计的固定特征，或驱动程序已保存当前的 IRQL。

如果已知的当前 IRQL 是调度\_级别，则调用方应设置此标志。 如果当前的 IRQL 未知，或调用方未在调度\_级别运行，则调用方应清除此标志。 如果调用方为 NDIS，则被调用函数应测试此标志，以避免更改 IRQL。

驱动程序不应测试 IRQL 来确定调度级别标志的值。 测试将违背标志的用途。 如有必要，被调用函数可以简单地执行测试。 驱动程序如何确定应该或不应该将标志设置为留给特定驱动程序的设计。

 

 





