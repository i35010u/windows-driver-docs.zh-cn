---
title: 与中断同步
description: 与中断同步
ms.assetid: f201acfa-98e4-4373-ba63-b6c814810f99
keywords:
- 中断 WDK 网络同步
- NdisMSynchronizeWithInterruptEx
- 同步 WDK 中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 882679d108e07f7ba1e00a36ffc5e525a57e2921
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362544"
---
# <a name="synchronizing-with-interrupts"></a>与中断同步





如果微型端口驱动程序[ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)函数与另一个共享资源，例如 NIC 寄存器或状态变量*MiniportXxx*在运行的函数降低 irql，因此， *MiniportXxx*函数必须调用[ **NdisMSynchronizeWithInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563681)。 此调用可确保微型端口驱动程序[ *MiniportSynchronizeInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559454)函数同步且包含多个处理器安全的方式可以访问共享的资源。

 

 





