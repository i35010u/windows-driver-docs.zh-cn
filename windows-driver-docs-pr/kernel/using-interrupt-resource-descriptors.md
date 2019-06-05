---
title: 使用中断资源描述符
description: 使用中断资源描述符
ms.assetid: 0e9aa9a1-c1aa-42e1-9c0b-a91a2424ad1a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 809bebef0b0b3652cf2f274dcb8717d9fa942681
ms.sourcegitcommit: 71c90354f7e2d88498e28f74fb1b34748edf82ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66491758"
---
# <a name="using-interrupt-resource-descriptors"></a>使用中断资源描述符


插即用 (PnP) 管理器将中断消息分配给设备使用了两个阶段。 首先，即插即用管理器发送[ **IRP\_MN\_筛选器\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff550874)驱动程序和硬件资源的列表的请求包括中断消息，它想要分配到设备。 该驱动程序可以修改此列表，以更改的中断消息数，以及每条消息的某些设置。 然后，实际分配资源的即插即用管理器后，将发送[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求并提供硬件的完整列表资源，包括中断消息，分配给驱动程序的设备。

**IRP\_MN\_筛选器\_资源\_要求**请求提供一系列[ **IO\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff550598)结构。 如果设备具有 MSI （消息信号中断） 功能结构 PCI 2.2 规范中定义，即插即用管理器提供单个中断消息描述符。 如果该设备已在 PCI 3.0 规范中定义的 MSI X 功能结构，即插即用管理器提供了一个结构的每个中断消息。 中断消息描述符具有**类型** = **CmResourceTypeInterrupt**并**标志**= CM\_资源\_中断\_LATCHED |CM\_资源\_中断\_消息。 驱动程序还可以通过更改来更改设置，如中断关联**u.Interrupt**结构的成员。 请注意，使用 MSI 时，中断所有具有相同关联，而使用 MSI X 时它们可以具有不同的相关性。 有关详细信息，请参阅[中断关联和优先级](interrupt-affinity-and-priority.md)。

对 PCI 2.2 中定义的 MSI **u.Interrupt.MaximumVector** - **u.Interrupt.MinimumVector** + 1 是为该设备分配的中断消息数。 驱动程序可以通过修改更改中断消息数**u.Interrupt.MinimumVector**。 对于 MSI 中断消息， **u.Interrupt.MaximumVector**始终是 CM\_资源\_中断\_消息\_令牌。 若要分配*MessageCount*中断消息，设置**u.Interrupt.MinimumVector**等于 CM\_资源\_中断\_消息\_令牌- *MessageCount* + 1。

对于 MSI X PCI 3.0 中定义的驱动程序可以更改分配通过添加或从列表中删除条目的中断消息数。 请注意必须随后在响应中删除该资源添加这种方式的中断消息[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 为 MSI X PnP 管理器提供了每个消息中断的一个描述符并**u.Interrupt.MinimumVector**并**u.Interrupt.MaximumVector**此描述符的成员将设置为 CM\_资源\_中断\_消息\_令牌。

一旦设备，包括中断消息的所有硬件资源都分配插管理器会将发送**IRP\_MN\_启动\_设备**向驱动程序的请求。 此请求提供的两个列表[ **CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构，分别对应于原始和已翻译资源。 对于中断消息，即插即用管理器提供一个与每个已分配的内存地址结构**类型** = **CmResourceTypeInterrupt**和**标志**= CM\_资源\_中断\_LATCHED |CM\_资源\_中断\_消息。

请注意，使用 MSI 时，该驱动程序只接收一个中断资源描述符，因为所有消息都共享同一地址。 **MessageCount**的成员**u.MessageInterrupt.Raw**可用于确定分配的消息数。 当使用 MSI X，驱动程序将接收每个中断消息的单独的资源描述符。

在 Windows 8 中，操作系统不支持资源请求超过 2048 个中断消息，每个设备函数。 在 Windows 7 和 Windows Vista 中，操作系统不支持的每个设备函数的多个 910 中断消息资源请求。 如果设备驱动程序超出此限制，则设备可能无法启动。 若要启用在包含多个逻辑处理器的计算机中运行的驱动程序，该驱动程序应避免请求每个处理器的多个中断。

在系统的中断资源重新平衡，过程即插即用管理器可能会要求驱动程序即可从资源要求列表中选择首选的一组备用中断资源。 但是，即插即用管理器不能始终将分配给驱动程序的驱动程序更适合于创建的资源。 该驱动程序因此必须承受，正常情况下，任何一组备用中断资源从资源请求列表的分配。 例如，设备可能会分配比请求的驱动程序较小数目的消息中断。 在最坏的情况下，驱动程序必须准备好运行只是一个基于行的中断的设备。

 

 




