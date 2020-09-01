---
title: 与 MSI 中断同步
description: 与 MSI 中断同步
ms.assetid: 61745a93-79dc-49ac-9ace-3ecb647b7b9a
keywords:
- MSI-X WDK 网络，同步中断
- 消息-已发出信号中断 WDK 网络，同步中断
- Msi WDK 网络，同步中断
- 中断 WDK 网络，同步
- 同步 WDK MSI-X
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78e7ca83159814c4df73a630fe8392287f674348
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207157"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>与 MSI 中断同步





如果微型端口驱动程序的 [*MiniportMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt) 函数共享资源（例如网络接口卡 (NIC) 寄存器或状态变量），并且另一个 *MiniportXxx* 函数以较低的 IRQL 运行，则其他 *MiniportXxx* 函数必须调用 [**NdisMSynchronizeWithInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex) 函数。 此调用可确保微型端口驱动程序的 [**MiniportSynchronizeMessageInterrupt**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt) 函数以同步且多处理器安全的方式访问共享资源。

 

