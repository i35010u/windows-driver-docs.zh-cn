---
title: 检索 IEEE 1394 节点的配置 ROM 的内容
description: Windows 7 包含使用内核模式驱动程序框架（KMDF）实现的1394ohci （一种新的 IEEE 1394 总线驱动程序）。
ms.assetid: AC327938-A813-4665-8E2E-43BEE11D4AA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 360e994f3ccada3d305a7869cf8bf23106bd5216
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841529"
---
# <a name="retrieving-the-contents-of-a-ieee-1394-nodes-configuration-rom"></a>检索 IEEE 1394 节点的配置 ROM 的内容


Windows 7 包含使用内核模式驱动程序框架（KMDF）实现的1394ohci （一种新的 IEEE 1394 总线驱动程序）。 1394ohci 总线驱动程序替换端口/微型端口配置中的旧版 IEEE bus 驱动程序--1394bus 和 ochi1394。 它与旧版1394总线驱动程序向后兼容。 有关新版本和旧1394总线驱动程序之间行为的一些已知差异的信息，请参阅[Windows 7 中的 IEEE 1394 总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)。

本主题提供有关1394ohci 总线驱动程序如何检索节点配置 ROM （稍后用于设备枚举）内容的详细信息。 对于 Windows 7，处理设备发现的节点配置 ROM 的内容未发生更改。 有关如何处理节点配置 ROM 内容的详细信息，请参阅[修改1394配置 rom](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-1394-configuration-rom)。

1394ohci 总线驱动程序通过将异步读取事务发送到节点，在1394总线重置后检索节点的配置 ROM 的内容。 它尝试减少发送到节点的异步读取事务数，以检索节点配置 ROM 的内容。

本主题包含以下各节：

-   [正在检索配置 ROM 标头](#retrieving-the-configuration-rom-header)
-   [新配置 ROM](#new-configuration-rom)
-   [以前检索到的配置 ROM](#previously-retrieved-configuration-rom)
-   [相关主题](#related-topics)

## <a name="retrieving-the-configuration-rom-header"></a>正在检索配置 ROM 标头


若要检索节点配置 ROM 的内容，客户端驱动程序通过将 GetLocalHostInformation 指定给**nLevel** ，将[**请求发送\_获取\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)1394 请求\_CONFIG\_ROM 获取\_主机。 完成请求后，总线驱动程序会在[**GET\_本地\_主机\_信息 5**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info5)结构中检索节点的配置 ROM 标头。 配置 ROM 标头位于节点配置 ROM 的前5个 quadlets。 此标头包含总线信息块的内容（如 IEEE-1394a 规范中所定义）。

1394ohci 总线驱动程序尝试在单个异步块读取事务中检索配置 ROM 标头。 但是，某些1394设备可能无法正确响应此事务。 在这种情况下，新的1394总线驱动程序使用五个异步 quadlet 读取事务来检索配置 ROM 标头。

在检索节点的配置 ROM 标头的过程中，将确定与节点的通信速度。 1394ohci 总线驱动程序以支持速度最快的速度将异步读取事务发送到节点，并考虑本地节点和目标节点之间的任何较慢的节点。 如果异步读取事务未以最快的支持速度完成，则1394ohci 总线驱动程序以较慢的速度向节点发送另一个异步读取事务。 在成功完成事务之前，1394ohci 总线驱动程序将继续以较慢和更慢的速度将异步读取事务发送到节点。 异步事务以特定速度完成后，会将该速度用于与该节点进行的所有其他通信，直到发生另一个1394总线重置。 如果异步读取事务未以速度最慢的速度完成，则1394ohci 总线驱动程序不会检索节点配置 ROM 的内容。

检索配置 ROM 标头后，1394ohci 总线驱动程序将检查是否之前已检索到节点的配置 ROM 的内容。 如果是这样，则可以重复使用其缓存版本。 否则，它必须检索节点配置 ROM 的其余内容。

## <a name="new-configuration-rom"></a>新配置 ROM


如果1394ohci 总线驱动程序确定先前未检索到节点配置 ROM 的内容，则会继续检索节点配置 ROM 的剩余内容。

1394ohci 总线驱动程序使用配置 ROM 标头的总线信息块中的**max\_rom**值来确定要发送到节点的异步读取事务的大小，以便检索配置的其余内容。CD-ROM. 如果任何异步读取事务失败，无论**最大\_rom**值如何—新的1394总线驱动程序都使用异步 quadlet 读取事务来检索节点配置 rom 的剩余内容。

## <a name="previously-retrieved-configuration-rom"></a>以前检索到的配置 ROM


1394ohci 总线驱动程序检索节点配置 ROM 标头的内容后，它会确定标头是否与驱动程序之前检索到的配置 ROM 内容的某个缓存副本的标头相匹配。 如果找到匹配的配置 ROM 标头，则会重复使用缓存的配置 ROM 内容。

1394ohci 总线驱动程序使用以下步骤来确定它是否可以重复使用节点配置 ROM 的内容的缓存副本：

1.  总线驱动程序确定节点的配置 ROM 标头的总线信息块中的**节点\_供应商\_id**、**芯片\_id hi**和**芯片\_id lo**值是否与标头中的相同值相匹配驱动程序的配置 ROM 内容的缓存副本之一。
2.  如果在步骤1中找到匹配项，则总线驱动程序将确定总线信息块中的生成值是否匹配。 如果代值未更改（或如果设置为1（表示它永远不会更改），则总线驱动程序将重用配置 ROM 的缓存内容。

可以在 IEEE 1394 规范的前面步骤中找到配置 ROM 值的说明。 如果1394ohci 总线驱动程序找不到匹配的缓存配置 ROM 标头，或者必须重新读取节点配置 ROM 的内容，因为**生成**值已更改，则将按照前面的步骤来检索的内容新配置 ROM。

## <a name="related-topics"></a>相关主题
[IEEE 1394 驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[修改 1394 配置 ROM](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-1394-configuration-rom)  
[**请求\_获取\_CONFIG\_ROM**](https://msdn.microsoft.com/library/windows/hardware/gg266404)  



