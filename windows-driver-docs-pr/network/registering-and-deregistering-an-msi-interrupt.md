---
title: 注册和取消注册 MSI 中断
description: 注册和取消注册 MSI 中断
ms.assetid: 61bdcf8c-b56e-4ef9-b9db-407591ff2f95
keywords:
- MSI-X WDK 网络，注册中断
- 消息-已发出信号中断 WDK 网络，注册中断
- Msi WDK 网络，注册中断
- 中断 WDK 网络，注册
- MSI-X WDK 网络，注销中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a47913fabc2a36dee974f38ff280b65bf799cb0b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212023"
---
# <a name="registering-and-deregistering-an-msi-interrupt"></a>注册和取消注册 MSI 中断





若要注册 MSI 支持，微型端口驱动程序会调用 [**NdisMRegisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex) 函数来注册 msi 中断。 驱动程序分配并初始化 [**NDIS \_ 微型端口 \_ 中断 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics) 结构，以指定中断特征和函数入口点。 驱动程序必须将 NDIS **MsiSupported** \_ 微型端口中断特征结构的 MsiSupported 成员设置 \_ \_ 为**TRUE**。 然后，该驱动程序将该结构传递给 **NdisMRegisterInterruptEx**。

必须定义以下函数以支持 MSI 中断：

-   [*MiniportMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)

-   [*MiniportMessageInterruptDpc*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)

-   [*MiniportDisableMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_message_interrupt)

-   [*MiniportEnableMessageInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_message_interrupt)

小型端口驱动程序应为基于行的中断函数提供入口点 (如以下列表所示) ，即使驱动程序支持 MSI 入口点也是如此。 如果 NDIS 未授予 MSI 中断，则可以将正常中断授予为回退条件。

行中断函数包括：

-   [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)

-   [*MiniportInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)

-   [*MiniportDisableInterruptEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_interrupt)

-   [*MiniportEnableInterruptEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_interrupt)

驱动程序应调用 [**NdisMDeregisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex) 函数来释放以前通过 **NdisMRegisterInterruptEx**分配的资源。

 

