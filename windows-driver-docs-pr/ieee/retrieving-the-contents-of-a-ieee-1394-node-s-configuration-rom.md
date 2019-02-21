---
title: 检索 IEEE 1394 节点的配置 ROM 的内容
description: Windows 7 包括 1394ohci.sys，新 IEEE 1394 总线驱动程序，通过使用内核模式驱动程序框架 (KMDF) 实现的。
ms.assetid: AC327938-A813-4665-8E2E-43BEE11D4AA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 469a4ebd97b0f47897e15d16a8dd8a6bf75be3e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523049"
---
# <a name="retrieving-the-contents-of-a-ieee-1394-nodes-configuration-rom"></a>检索 IEEE 1394 节点的配置 ROM 的内容


Windows 7 包括 1394ohci.sys，新 IEEE 1394 总线驱动程序，通过使用内核模式驱动程序框架 (KMDF) 实现的。 1394ohci.sys 总线驱动程序将替换中端口/微型端口配置-1394bus.sys 和 ochi1394.sys 的旧 IEEE 总线驱动程序。 它是与旧的 1394年总线驱动程序向后兼容。 有关一些新的和旧的 1394年总线驱动程序之间已知的行为差异的信息，请参阅[IEEE 1394 总线驱动程序在 Windows 7 中](https://msdn.microsoft.com/library/windows/hardware/gg266402)。

本主题提供有关如何 1394ohci.sys 总线驱动程序检索节点的配置 ROM，更高版本用于设备枚举中的内容的详细信息。 适用于 Windows 7 未更改处理的节点配置 ROM 设备发现的内容。 有关如何处理节点的配置 ROM 的内容的详细信息，请参阅[修改 1394年配置 ROM](https://msdn.microsoft.com/library/windows/hardware/ff537433)。

1394ohci.sys 总线驱动程序检索节点的配置 ROM 中的内容之后的 1394年总线重置通过发送异步读取到的节点的事务。 它将尝试减少发送到的节点来检索节点的配置 rom。 内容的异步读取事务数

本主题包含以下各节：

-   [检索配置 ROM 标头](#retrieving-the-configuration-rom-header)
-   [新配置 ROM](#new-configuration-rom)
-   [以前检索到配置 ROM](#previously-retrieved-configuration-rom)
-   [相关的主题](#related-topics)

## <a name="retrieving-the-configuration-rom-header"></a>检索配置 ROM 标头


若要检索的节点的配置 ROM 内容，客户端驱动程序发送[**请求\_获取\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)请求到通过指定的 IEEE 1394 驱动程序堆栈**u.GetLocalHostInformation.nLevel**与 GET\_主机\_配置\_rom。 在完成请求，请总线驱动程序检索节点的配置 ROM 中的标头[**获取\_本地\_主机\_INFO5** ](https://msdn.microsoft.com/library/windows/hardware/ff537152)结构。 配置 ROM 标头是配置的在前五个 quadlets 的节点 rom。 此标头包括总线信息块，内容在 IEEE 1394a 规范中定义。

1394ohci.sys 总线驱动程序尝试检索配置 ROM 标头中读取事务是一个异步块。 但是，某些 1394年设备可能不响应为此事务正确。 在此情况下，新的 1394年总线驱动程序使用五个读取事务的异步 quadlet 检索配置 ROM 标头。

与节点进行通信的速度取决于节点的配置 ROM 标头的检索过程。 1394ohci.sys 总线驱动程序将异步读取的事务发送到的速度最快受支持的节点，并考虑本地节点和目标节点之间任何速度较慢的节点。 如果异步读取事务未成功完成的速度最快受支持，然后 1394ohci.sys 总线驱动程序将发送另一次异步读取速度较慢的节点的事务。 1394ohci.sys 总线驱动程序将继续将异步读取的事务发送到的速度较慢且速度较慢的节点，直到成功完成事务。 在特定的速度，速度是用于完成异步事务后会发生与另一个的 1394年总线重置之前的节点的所有其他通信。 如果异步读取事务未完成的速度最慢可能，则 1394ohci.sys 总线驱动程序不会检索内容节点的配置 rom。

检索配置 ROM 标头后，1394ohci.sys 总线驱动程序将检查是否以前检索到的节点的配置 ROM 内容。 如果是这样，它可以重复使用其缓存的版本。 否则，它必须检索的节点的配置 rom。 剩余的内容

## <a name="new-configuration-rom"></a>新配置 ROM


如果 1394ohci.sys 总线驱动程序确定，ROM 以前未检索到的节点上配置的内容，它继续检索的节点的配置 rom。 剩余的内容

1394ohci.sys 总线驱动程序将使用**最大\_rom**读取事务发送到的节点来检索剩余配置 ROM 标头，以确定异步大小的总线信息块中的值配置 rom。 的内容 如果任何异步读取的事务失败，而不考虑**最大\_rom**值 — 新的 1394年总线驱动程序使用异步 quadlet 读取的事务来检索的节点的配置 rom。 剩余的内容

## <a name="previously-retrieved-configuration-rom"></a>以前检索到配置 ROM


1394ohci.sys 总线驱动程序检索节点的配置 ROM 标头的内容后，它确定标头是否与驱动程序以前检索到的配置 ROM 内容的缓存副本之一的标头相匹配。 如果它找到匹配的配置 ROM 标头，它重用缓存的配置 ROM 内容。

1394ohci.sys 总线驱动程序使用以下步骤来确定是否可以重复使用的节点的配置 ROM 内容的缓存的副本：

1.  总线驱动程序确定是否**节点\_供应商\_id**，**芯片\_id 大家好**，并且**芯片\_id lo**节点的配置 ROM 标头的总线信息块中的值匹配的一个驱动程序的缓存副本配置 ROM 内容的标头中这些相同的值。
2.  如果在找到匹配项的步骤 1，则总线驱动程序确定是否也与匹配总线信息块中的生成值。 如果未更改的生成值 （或如果设置为 1，表示将永远不会更改），然后总线驱动程序重用缓存的内容的配置 rom。

中的 IEEE 1394 规范中的上一步骤中，找到的配置说明 ROM 值。 如果 1394ohci.sys 总线驱动程序未能找到匹配的缓存配置 ROM 标头，或因为，它必须重新读取的内容节点的配置 ROM**生成**值发生更改，将遵循到前面的步骤检索内容的新配置 rom。

## <a name="related-topics"></a>相关主题
[IEEE 1394 驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/ff538867)  
[修改 1394年配置 ROM](https://msdn.microsoft.com/library/windows/hardware/ff537433)  
[**REQUEST\_GET\_CONFIG\_ROM**](https://msdn.microsoft.com/library/windows/hardware/gg266404)  



