---
title: 与 MSI 中断同步
description: 与 MSI 中断同步
ms.assetid: 61745a93-79dc-49ac-9ace-3ecb647b7b9a
keywords:
- MSI X WDK 连接网络、 同步中断
- 消息信号中断 WDK 网络同步中断
- Msi WDK 网络同步中断
- 中断 WDK 网络同步
- 同步 WDK MSI X
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd290096f040f4bffeb35d961fe574dc6024dfca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377957"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>与 MSI 中断同步





如果微型端口驱动程序[ *MiniportMessageInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)函数与另一个共享资源，例如网络接口卡 (NIC) 寄存器或状态变量*MiniportXxx*运行在较低的 IRQL，其他函数*MiniportXxx*函数必须调用[ **NdisMSynchronizeWithInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsynchronizewithinterruptex)函数。 此调用可确保微型端口驱动程序[ **MiniportSynchronizeMessageInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_synchronize_interrupt)函数同步且包含多个处理器安全的方式可以访问共享的资源。

 

 





