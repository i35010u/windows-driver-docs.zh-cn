---
title: 动态配置 MSI-X
description: 动态配置 MSI-X
ms.assetid: 53051239-e00f-41e8-b95d-9618693e696d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 77224c97a6b63e4e890d59cf2205ea177561bad6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838712"
---
# <a name="dynamically-configuring-msi-x"></a>动态配置 MSI-X


Windows Vista Service Pack 1 （SP1）、Windows Server 2008 和更高版本的操作系统支持动态修改 MSI X 中断消息的属性。 （PCI 3.0 规范定义的 MSI-X。）PCI 总线驱动程序公开 GUID\_.MSIX\_表\_CONFIG\_接口接口，以允许 PCI 设备的驱动程序修改总线硬件中断表中的设置。

驱动程序使用接口，方法是将[**IRP\_MN\_QUERY\_interface**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)请求发送到总线驱动程序，将*INTERFACETYPE*参数等于 GUID\_.MSIX\_\_\_interface。 总线驱动程序提供指向[**PCI\_.msix\_表\_CONFIG\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pci_msix_table_config_interface)结构的指针，该接口提供指向三个用于修改中断表的例程的指针：

-   [*SetTableEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pci_msix_set_entry)将消息 ID 分配给硬件表条目。

-   [*MaskTableEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pci_msix_maskunmask_entry)屏蔽对应于硬件表条目的中断。

-   [*UnmaskTableEntry*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/gg604859(v=vs.85))解除对应于硬件表条目的中断。

默认情况下，会对中断表进行配置，以便第一个条目的消息 ID 为0，第二个条目的消息 ID 为1，依此类推。 如果表项的数目超过消息数，则为每个附加表项分配消息 ID 零。 （消息 ID 是 IO\_中断的**MessageInfo**成员中的中断条目的索引[ **\_消息\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_interrupt_message_info)描述驱动程序的消息终止中断的信息结构。 [**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)例程提供指向此结构的指针。）

 

 




