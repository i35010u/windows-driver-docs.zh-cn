---
title: 注册和取消注册中断
description: 注册和取消注册中断
keywords:
- 中断 WDK 网络，注册
- 中断 WDK 网络，注销
- NdisMRegisterInterruptEx
- NdisMDeregisterInterruptEx
- 注册中断
- 注销中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b719aca3c948ee4826914f266515bfbd5f8c5486
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838555"
---
# <a name="registering-and-deregistering-interrupts"></a>注册和取消注册中断





微型端口驱动程序调用 [**NdisMRegisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex) 来注册中断。 驱动程序分配并初始化 [**NDIS \_ 微型端口 \_ 中断 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics) 结构，以指定中断特征和函数入口点。 驱动程序将该结构传递给 **NdisMRegisterInterruptEx**。

驱动程序调用 [**NdisMDeRegisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex) 函数来释放以前通过 **NdisMRegisterInterruptEx** 分配的资源。

 

