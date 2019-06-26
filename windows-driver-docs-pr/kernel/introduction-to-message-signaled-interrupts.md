---
title: 消息信号中断简介
description: 消息信号中断简介
ms.assetid: 035207a1-762d-463e-822e-64ac4833afa4
keywords:
- 消息信号中断 WDK 内核
- Msi WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9110bf7890c3d370c9e636eb6725e2c9e01dfbe5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369931"
---
# <a name="introduction-to-message-signaled-interrupts"></a>消息信号中断简介


作为基于行的中断的替代方法的 PCI 2.2 规范中引入了消息信号中断 (Msi)。 而不是使用专用的 pin 来触发中断，设备使用 Msi 通过写入到特定内存地址的值来触发中断。 PCI 3.0 定义名为的 msi 的扩展窗体*MSI X*，使更大的可编程性。 Windows Vista 和更高版本的 Windows 支持 MSI 和 MSI X。 一台设备可以支持 MSI 和 MSI X。 对于此类设备，操作系统将自动使用 MSI X。

*中断消息*是一个特定值，设备将写入到特定地址触发中断。 与基于行的中断消息信号中断具有边缘语义。 设备发送一条消息，但不会接收任何硬件确认收到中断。

PCI 2.2 一条消息包含的地址和部分不透明的 16 位值。 每个设备分配一个地址。 若要发送多条消息，设备可以使用较低的消息值的 4 位来区分消息。 因此，对于 PCI 2.2 设备可以支持最多 16 条消息。

对于 PCI 3.0 来说，一条消息包含的地址和一个不透明的 32 位值。 每个不同的消息都有其自己唯一的地址。 与不同的 PCI 2.2，设备不会修改值。 PCI 3.0 设备可以支持最多 2048 个不同的消息。 支持 PCI 3.0 MSI-X 的设备功能的中断源设备中的每个包含条目的动态可编程硬件表。 此表中的每个条目可以使用其中一条消息，将分配到一台设备，并且可以独立地屏蔽编程。 驱动程序可以更改表项和条目是否已屏蔽的中断消息的编程。 有关详细信息，请参阅[动态配置 MSI-X](dynamically-configuring-msi-x.md)。

驱动程序可以注册单个[ *InterruptMessageService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)例程处理的所有可能的消息或个人[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)为每个消息的例程。

驱动程序可以处理设备发送，如下所示的 Msi:

1.  在驱动程序安装过程中启用 msi，然后在注册表中。 此外可以使用注册表来指定要分配的设备的消息数。 有关详细信息，请参阅[Enabling Message-Signaled 中断在注册表中](enabling-message-signaled-interrupts-in-the-registry.md)。

2.  （可选） 增加的中断消息数并将每条消息的某些设置保存回应[ **IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)请求。 有关详细信息，请参阅[使用 Interrupt 资源描述符](using-interrupt-resource-descriptors.md)。

3.  中的驱动程序的调度例程[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)，调用[ **IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)注册*InterruptService*或*InterruptMessageService*例程，以服务设备的中断。 使用 CONNECT\_完全\_的指定版本**IoConnectInterruptEx**注册*InterruptService*例程特定的消息或连接\_消息\_基于版本**IoConnectInterruptEx**注册单个*InterruptMessageService*例程的所有消息。 有关详细信息，请参阅[使用 CONNECT\_消息\_基于版本的 IoConnectInterruptEx](using-the-connect-message-based-version-of-ioconnectinterruptex.md)并[使用 CONNECT\_完全\_指定版本IoConnectInterruptEx](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)。

4.  该驱动程序不能再想服务中断从设备后，调用[ **IoDisconnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterruptex) （之后禁用设备的中断） 中删除任何已注册的中断服务例程。

旨在使用多个消息的驱动程序应检查，分配给预期的消息数。 如果插即用 (PnP) 管理器无法分配请求的数目的消息，它而是会分配到设备的一个消息。 驱动程序可以检查实际分配通过以下方式之一的消息数：

-   PnP 管理器报告其原始资源描述符的列表中的已分配消息数。 有关详细信息，请参阅[使用 Interrupt 资源描述符](using-interrupt-resource-descriptors.md)。

-   当**IoConnectInterruptEx**返回时，它会设置*参数*-&gt;**MessageBased.ConnectContext.InterruptMessageTable-&gt;MessageCount**到分配的消息数。

 

 




