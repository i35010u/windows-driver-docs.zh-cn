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
ms.openlocfilehash: c52f9b95ccebec27f59f1fae48541312fbd7d7f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842091"
---
# <a name="registering-and-deregistering-an-msi-interrupt"></a>注册和取消注册 MSI 中断





若要注册 MSI 支持，微型端口驱动程序会调用[**NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)函数来注册 msi 中断。 驱动程序将[ **\_微型端口分配和初始化 NDIS，\_中断\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_interrupt_characteristics)结构来指定中断特征和函数入口点。 驱动程序必须将 NDIS\_微型端口\_中断\_特征结构的**MsiSupported**成员设置为**TRUE**。 然后，该驱动程序将该结构传递给**NdisMRegisterInterruptEx**。

必须定义以下函数以支持 MSI 中断：

-   [*MiniportMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)

-   [*MiniportMessageInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)

-   [*MiniportDisableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_message_interrupt)

-   [*MiniportEnableMessageInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_message_interrupt)

小型端口驱动程序应为基于行的中断函数提供入口点（如下表中所示），即使驱动程序支持 MSI 入口点也是如此。 如果 NDIS 未授予 MSI 中断，则可以将正常中断授予为回退条件。

行中断函数包括：

-   [*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)

-   [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)

-   [*MiniportDisableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_disable_interrupt)

-   [*MiniportEnableInterruptEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_enable_interrupt)

驱动程序应调用[**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)函数来释放以前通过**NdisMRegisterInterruptEx**分配的资源。

 

 





