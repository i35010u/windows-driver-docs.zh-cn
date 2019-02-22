---
title: 动态配置 MSI X
description: 动态配置 MSI X
ms.assetid: 53051239-e00f-41e8-b95d-9618693e696d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 564c18d512d23ab7372d7ab089e570b47ea7658a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522512"
---
# <a name="dynamically-configuring-msi-x"></a>动态配置 MSI X


Windows Vista Service Pack 1 (SP1)、 Windows Server 2008 和更高版本的操作系统支持动态修改 MSI X 中断消息的属性。 （PCI 3.0 规范定义 MSI X。）PCI 总线驱动程序公开 GUID\_MSIX\_表\_CONFIG\_接口接口，以允许修改总线硬件中断表中的设置的 PCI 设备的驱动程序。

驱动程序通过发送使用界面[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求到总线驱动程序，使用*InterfaceType*参数等于 GUID\_MSIX\_表\_配置\_接口。 总线驱动程序提供一个指向[ **PCI\_MSIX\_表\_CONFIG\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff558787)结构，它提供三个例程的指针修改中断表：

-   [*SetTableEntry* ](https://msdn.microsoft.com/library/windows/hardware/gg604857)将消息 ID 分配给硬件表条目。

-   [*MaskTableEntry* ](https://msdn.microsoft.com/library/windows/hardware/gg604852)屏蔽与硬件表条目相对应的中断。

-   [*UnmaskTableEntry* ](https://msdn.microsoft.com/library/windows/hardware/gg604859)解除屏蔽的中断与硬件表条目相对应。

默认情况下，中断表已配置，以便第一个条目都具有消息 ID 为零，第二个条目具有消息 ID，等等。 如果表条目数超过消息数，每个其他表条目分配消息 ID 为零。 (消息 ID 是中的中断的项的索引**MessageInfo**的成员[ **IO\_中断\_消息\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff550576)结构，描述驱动程序的消息信号中断。 [ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)例程提供指向此结构的指针。)

 

 




