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
ms.openlocfilehash: edfd8ab179f6ca60e18aedb4aa6b369224308e33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841787"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>与 MSI 中断同步





如果微型端口驱动程序的[*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)函数共享资源（例如网络接口卡（NIC）寄存器或状态变量），而另一个*MiniportXxx*函数运行在较低的 IRQL 下，另一个*MiniportXxx*函数必须调用[**NdisMSynchronizeWithInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)函数。 此调用可确保微型端口驱动程序的[**MiniportSynchronizeMessageInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_synchronize_interrupt)函数以同步且多处理器安全的方式访问共享资源。

 

 





