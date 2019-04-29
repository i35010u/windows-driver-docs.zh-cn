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
ms.openlocfilehash: 8a8ed85eac6e133b6a9da0962c5f03f078eaa28a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362541"
---
# <a name="synchronizing-with-an-msi-interrupt"></a>与 MSI 中断同步





如果微型端口驱动程序[ *MiniportMessageInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559407)函数与另一个共享资源，例如网络接口卡 (NIC) 寄存器或状态变量*MiniportXxx*运行在较低的 IRQL，其他函数*MiniportXxx*函数必须调用[ **NdisMSynchronizeWithInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563681)函数。 此调用可确保微型端口驱动程序[ **MiniportSynchronizeMessageInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff559455)函数同步且包含多个处理器安全的方式可以访问共享的资源。

 

 





