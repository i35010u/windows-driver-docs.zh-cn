---
title: 动态配置 MSI-X
description: 动态配置 MSI-X
ms.assetid: 53051239-e00f-41e8-b95d-9618693e696d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ec25b844e9097b1c8c7286a8b5f6298ae3a84e0f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190713"
---
# <a name="dynamically-configuring-msi-x"></a>动态配置 MSI-X


Windows Vista Service Pack 1 (SP1) 、Windows Server 2008 和更高版本的操作系统支持动态修改 MSI X 中断消息的属性。  (PCI 3.0 规范定义的 MSI-X。 ) PCI 总线驱动程序公开 GUID \_ .Msix \_ 表 \_ 配置 \_ 接口接口，以允许 PCI 设备的驱动程序修改总线硬件中断表中的设置。

驱动程序通过将 [**IRP \_ MN \_ 查询 \_ 接口**](./irp-mn-query-interface.md) 请求发送到总线驱动程序来使用接口， *InterfaceType* 参数等于 GUID \_ .msix \_ 表 \_ 配置 \_ 接口。 总线驱动程序提供了一个指向 [**PCI \_ .Msix \_ 表 \_ 配置 \_ 接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pci_msix_table_config_interface) 结构的指针，该结构提供了指向三个用于修改中断表的例程的指针：

-   [*SetTableEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-pci_msix_set_entry) 将消息 ID 分配给硬件表条目。

-   [*MaskTableEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-pci_msix_maskunmask_entry) 屏蔽对应于硬件表条目的中断。

-   [*UnmaskTableEntry*](/previous-versions/windows/hardware/drivers/gg604859(v=vs.85)) 解除对应于硬件表条目的中断。

默认情况下，会对中断表进行配置，以便第一个条目的消息 ID 为0，第二个条目的消息 ID 为1，依此类推。 如果表项的数目超过消息数，则为每个附加表项分配消息 ID 零。  (消息 ID 是用于描述驱动程序的消息终止中断的[**IO \_ 中断 \_ 消息 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_interrupt_message_info)结构的**MessageInfo**成员中的中断条目的索引。 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)例程提供指向此结构的指针。 ) 

 

