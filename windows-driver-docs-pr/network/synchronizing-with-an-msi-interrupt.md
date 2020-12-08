---
title: 与 MSI 中断同步
description: 与 MSI 中断同步
keywords:
- MSI-X WDK 网络，同步中断
- 消息-已发出信号中断 WDK 网络，同步中断
- Msi WDK 网络，同步中断
- 中断 WDK 网络，同步
- 同步 WDK MSI-X
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06b3b838ab5e95065e2670d6c2e502df5db45efd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802275"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>与 MSI 中断同步





如果微型端口驱动程序的 [*MiniportMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt) 函数共享资源（例如网络接口卡 (NIC) 寄存器或状态变量），并且另一个 *MiniportXxx* 函数以较低的 IRQL 运行，则其他 *MiniportXxx* 函数必须调用 [**NdisMSynchronizeWithInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex) 函数。 此调用可确保微型端口驱动程序的 [**MiniportSynchronizeMessageInterrupt**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt) 函数以同步且多处理器安全的方式访问共享资源。

 

