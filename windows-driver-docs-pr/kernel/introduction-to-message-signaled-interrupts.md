---
title: 消息信号中断简介
description: 消息信号中断简介
ms.assetid: 035207a1-762d-463e-822e-64ac4833afa4
keywords:
- 消息-已发出信号中断 WDK 内核
- Msi WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa41f84a55415070c884bc5d916c82d0ddf1fef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828192"
---
# <a name="introduction-to-message-signaled-interrupts"></a>消息信号中断简介


在 PCI 2.2 规范中引入了消息信号中断（Msi）作为基于行的中断的替代方法。 使用 Msi 的设备会通过将值写入特定内存地址来触发中断，而不是使用专用的 pin 来触发中断。 PCI 3.0 定义了一个名为的 msi 扩展*形式，它*可以实现更强的编程能力。 Windows Vista 和更高版本的 Windows 支持 MSI 和 MSI-X。 单个设备可以支持 MSI 和 MSI-X。 对于这种设备，操作系统将自动使用 MSI-X。

*中断消息*是设备写入特定地址以触发中断的特定值。 与基于行的中断不同，消息信号中断具有边缘语义。 设备发送一条消息，但不会收到收到中断的任何硬件确认。

对于 PCI 2.2，消息由地址和部分不透明的16位值组成。 为每个设备分配一个地址。 若要发送多条消息，设备可以使用消息值的低4位来区分消息。 因此，对于 PCI 2.2，设备最多可支持16条消息。

对于 PCI 3.0，消息包含一个地址和一个不透明的32位值。 每个不同的消息都有其自己的唯一地址。 与 PCI 2.2 不同，设备不会修改此值。 对于 PCI 3.0，设备最多可以支持2048个不同的消息。 支持 PCI 3.0 MSI X 的设备功能是一个动态可编程的硬件表，其中包含设备中每个中断源的条目。 此表中的每个条目都可以使用分配给设备的一条消息进行编程，并可以单独屏蔽。 驱动程序可以将中断消息的编程更改为表项以及是否屏蔽了某个条目。 有关详细信息，请参阅[动态配置 MSI-X](dynamically-configuring-msi-x.md)。

驱动程序可以注册单个[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)例程来处理每条消息的所有可能的消息或单个[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程。

驱动程序可以处理设备发送的 Msi，如下所示：

1.  在驱动程序安装过程中，请在注册表中启用 Msi。 你还可以使用注册表来指定要为设备分配的消息数。 有关详细信息，请参阅[启用注册表中的消息终止中断](enabling-message-signaled-interrupts-in-the-registry.md)。

2.  （可选）通过响应[**IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)请求，增加中断消息的数目并保存某些每个消息的设置。 有关详细信息，请参阅[使用中断资源描述符](using-interrupt-resource-descriptors.md)。

3.  在用于 IRP\_MN 的驱动程序调度例程[ **\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)上，调用[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)来注册*InterruptService*或*InterruptMessageService*例程以为设备的中断提供服务. 使用连接\_完全\_指定版本的**IoConnectInterruptEx**为特定消息注册*InterruptService*例程，\_或使用 IoConnectInterruptEx 的消息\_为所有消息注册单个*InterruptMessageService*例程。 有关详细信息，请参阅[使用连接\_消息\_IoConnectInterruptEx 版本](using-the-connect-message-based-version-of-ioconnectinterruptex.md)，并[使用连接\_完全\_指定的 IoConnectInterruptEx 版本](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)。

4.  驱动程序不再打算从设备中服务中断后，调用[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex) （禁用设备的中断后）以删除任何已注册的中断服务例程。

旨在使用多条消息的驱动程序应检查是否分配了预期的消息数。 如果即插即用（PnP）管理器无法分配请求的消息数，则只向设备分配一条消息。 驱动程序可以通过下列方式之一来检查实际分配的消息数：

-   PnP 管理器在其原始资源描述符列表中报告分配的消息数。 有关详细信息，请参阅[使用中断资源描述符](using-interrupt-resource-descriptors.md)。

-   当**IoConnectInterruptEx**返回时，它会将*参数*-&gt;**InterruptMessageTable-&gt;MessageCount**设置为分配的消息数。

 

 




