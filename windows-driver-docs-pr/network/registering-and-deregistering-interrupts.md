---
title: 注册和取消注册中断
description: 注册和取消注册中断
ms.assetid: 222782f3-092e-417d-ab1b-1988a593caa4
keywords:
- 中断 WDK 连接网络、 注册
- 中断 WDK 连接网络、 取消注册
- NdisMRegisterInterruptEx
- NdisMDeregisterInterruptEx
- 注册中断
- 取消中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29b1d747ae387270af0d73aeee2f339b2a6ab31b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359174"
---
# <a name="registering-and-deregistering-interrupts"></a>注册和取消注册中断





微型端口驱动程序调用[ **NdisMRegisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterinterruptex)注册中断。 该驱动程序分配并初始化[ **NDIS\_微型端口\_中断\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)结构，以指定中断特征和函数入口点。 该驱动程序将向此结构传递**NdisMRegisterInterruptEx**。

驱动程序调用[ **NdisMDeRegisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)函数，以释放以前分配的资源**NdisMRegisterInterruptEx**。

 

 





