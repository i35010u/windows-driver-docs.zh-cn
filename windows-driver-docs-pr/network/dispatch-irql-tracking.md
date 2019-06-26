---
title: 调度 IRQL 跟踪
description: 调度 IRQL 跟踪
ms.assetid: ac559f4f-0138-4b9a-8f1b-44a2973fd6a1
keywords:
- 调度级别标志 WDK 网络
- 于 Irql WDK 网络
- 网络驱动程序 WDK，于 Irql
- 当前于 Irql WDK 网络
- 调度 IRQL 跟踪 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61daa1c24766a6d7907016b9e640d1a6256792a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386566"
---
# <a name="dispatch-irql-tracking"></a>调度 IRQL 跟踪





若要提高系统性能，某些 NDIS 函数 (例如， [ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)函数) 包括一个调度级别标志，指示当前 IRQL。 正确使用调度级别标志有助于避免不必要设置 IRQL 的尝试。

用于控制其他属性的其他标志，但调度级别标志的名称是：

NDIS\_发送\_标志\_调度\_级别

NDIS\_发送\_完成\_标志\_调度\_级别

NDIS\_接收\_标志\_调度\_级别

NDIS\_返回\_标志\_调度\_级别

NDIS\_RWL\_处\_调度\_级别

调用方必须通过测试 IRQL 不确定从已知的当前 IRQL，调度级别标志设置。 例如，因为它是驱动程序设计的一个固定的特征或该驱动程序保存当前 IRQL 知道 IRQL。

如果已知当前 IRQL 调度\_级别，调用方应设置此标志。 如果当前 IRQL 为未知的或调用方未运行在调度\_级别，调用方应清除此标志。 如果调用方是 NDIS，所调用的函数应测试此标志，以避免更改的 IRQL。

驱动程序不应测试的 IRQL 来确定调度级别标志的值。 测试将违背标志的用途。 如有必要，可以只需测试本身执行调用的函数。 驱动程序如何确定它应该或不应将该标志设置为从左到特定的驱动程序的设计。

 

 





