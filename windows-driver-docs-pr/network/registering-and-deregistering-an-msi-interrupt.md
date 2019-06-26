---
title: 注册和取消注册 MSI 中断
description: 注册和取消注册 MSI 中断
ms.assetid: 61bdcf8c-b56e-4ef9-b9db-407591ff2f95
keywords:
- MSI X WDK 连接网络、 注册中断
- 消息信号中断 WDK 网络注册中断
- Msi WDK 网络注册中断
- 中断 WDK 连接网络、 注册
- MSI X WDK 连接网络、 取消的中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02627f2084f59631c1e1cbf7e443a0a61ab7ef84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374785"
---
# <a name="registering-and-deregistering-an-msi-interrupt"></a>注册和取消注册 MSI 中断





若要注册 MSI 的支持，微型端口驱动程序调用[ **NdisMRegisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterinterruptex)函数以注册 MSI 中断。 该驱动程序分配并初始化[ **NDIS\_微型端口\_中断\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)结构，以指定中断特征和函数入口点。 该驱动程序必须设置**MsiSupported**成员的 NDIS\_微型端口\_中断\_特征结构**TRUE**。 该驱动程序然后将传递的结构**NdisMRegisterInterruptEx**。

必须定义以下函数以支持 MSI 中断：

-   [*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt)

-   [*MiniportMessageInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt_dpc)

-   [*MiniportDisableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_disable_message_interrupt)

-   [*MiniportEnableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_enable_message_interrupt)

微型端口驱动程序应为基于行的中断函数 （它们以下列表中所示），提供入口点，即使该驱动程序支持 MSI 入口点。 如果 NDIS 不会授予 MSI 中断，它可以作为回退条件授予正常中断。

行中断函数包括：

-   [*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)

-   [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)

-   [*MiniportDisableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_disable_interrupt)

-   [*MiniportEnableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_enable_interrupt)

驱动程序应调用[ **NdisMDeregisterInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)函数，以释放以前分配的资源**NdisMRegisterInterruptEx**。

 

 





