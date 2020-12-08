---
title: 检索 IEEE 1394 节点的配置 ROM 的内容
description: Windows 7 包括 1394ohci.sys （一种新的 IEEE 1394 总线驱动程序），该驱动程序通过使用内核模式驱动程序框架 (KMDF) 实现。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c272983ffb1d871eba31c166c096b382ffb29f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815400"
---
# <a name="retrieving-the-contents-of-a-ieee-1394-nodes-configuration-rom"></a>检索 IEEE 1394 节点的配置 ROM 的内容


Windows 7 包括 1394ohci.sys （一种新的 IEEE 1394 总线驱动程序），该驱动程序通过使用内核模式驱动程序框架 (KMDF) 实现。 1394ohci.sys 总线驱动程序替换端口/微型端口配置中的旧版 IEEE bus 驱动程序--1394bus.sys 和 ochi1394.sys。 它与旧版1394总线驱动程序向后兼容。 有关新版本和旧1394总线驱动程序之间行为的一些已知差异的信息，请参阅 [Windows 7 中的 IEEE 1394 总线驱动程序](./ieee-1394-bus-driver-in-windows-7.md)。

本主题提供有关 1394ohci.sys 总线驱动程序如何检索节点配置 ROM （稍后用于设备枚举）内容的详细信息。 对于 Windows 7，处理设备发现的节点配置 ROM 的内容未发生更改。 有关如何处理节点配置 ROM 内容的详细信息，请参阅 [修改1394配置 rom](./modifying-the-1394-configuration-rom.md)。

1394ohci.sys 总线驱动程序通过将异步读取事务发送到节点，在1394总线重置后检索节点的配置 ROM 的内容。 它尝试减少发送到节点的异步读取事务数，以检索节点配置 ROM 的内容。

本主题包含以下各节：

-   [正在检索配置 ROM 标头](#retrieving-the-configuration-rom-header)
-   [新配置 ROM](#new-configuration-rom)
-   [以前检索到的配置 ROM](#previously-retrieved-configuration-rom)
-   [相关主题](#related-topics)

## <a name="retrieving-the-configuration-rom-header"></a>正在检索配置 ROM 标头


若要检索节点配置 ROM 的内容，客户端驱动程序通过指定 **GetLocalHostInformation NLEVEL** 获取主机配置 rom，将 [**请求 \_ 获取 \_ 本地 \_ 主机 \_ 信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)请求发送到 IEEE 1394 驱动程序堆栈 \_ \_ \_ 。 完成请求后，总线驱动程序会在 [**GET \_ LOCAL \_ HOST \_ 信息 5**](/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info5) 结构中检索节点的配置 ROM 标头。 配置 ROM 标头位于节点配置 ROM 的前5个 quadlets。 此标头包含总线信息块的内容（如 IEEE-1394a 规范中所定义）。

1394ohci.sys 总线驱动程序尝试在单个异步块读取事务中检索配置 ROM 标头。 但是，某些1394设备可能无法正确响应此事务。 在这种情况下，新的1394总线驱动程序使用五个异步 quadlet 读取事务来检索配置 ROM 标头。

在检索节点的配置 ROM 标头的过程中，将确定与节点的通信速度。 1394ohci.sys 总线驱动程序以支持速度最快的速度将异步读取事务发送到节点，并考虑本地节点和目标节点之间的任何较慢的节点。 如果异步读取事务未以最快的支持速度完成，则 1394ohci.sys 总线驱动程序以较慢的速度向节点发送另一个异步读取事务。 在成功完成事务之前，1394ohci.sys 总线驱动程序将继续以较慢和较慢的速度将异步读取事务发送到节点。 异步事务以特定速度完成后，会将该速度用于与该节点进行的所有其他通信，直到发生另一个1394总线重置。 如果异步读取事务未以速度最慢的速度完成，则 1394ohci.sys 总线驱动程序不会检索节点配置 ROM 的内容。

检索配置 ROM 标头后，1394ohci.sys 总线驱动程序将检查是否之前已检索到节点的配置 ROM 的内容。 如果是这样，则可以重复使用其缓存版本。 否则，它必须检索节点配置 ROM 的其余内容。

## <a name="new-configuration-rom"></a>新配置 ROM


如果 1394ohci.sys 总线驱动程序确定先前未检索到节点配置 ROM 的内容，则会继续检索节点配置 ROM 的剩余内容。

1394ohci.sys 总线驱动程序使用配置 ROM 标头的总线信息块中的 **最大 \_ rom** 值来确定要发送到节点的异步读取事务的大小，以便检索配置 rom 的剩余内容。 如果任何异步读取事务失败（无论 **最大 \_ rom** 值如何），则新的1394总线驱动程序将使用异步 quadlet 读取事务来检索节点配置 rom 的剩余内容。

## <a name="previously-retrieved-configuration-rom"></a>以前检索到的配置 ROM


1394ohci.sys 总线驱动程序检索到节点的配置 ROM 标头的内容后，它将确定标头是否与驱动程序之前检索到的配置 ROM 内容的某个缓存副本的标头相匹配。 如果找到匹配的配置 ROM 标头，则会重复使用缓存的配置 ROM 内容。

1394ohci.sys 总线驱动程序使用以下步骤来确定它是否可以重复使用节点配置 ROM 的内容的缓存副本：

1.  总线驱动程序确定节点的配置 ROM 标头的总线信息块中的 **节点 \_ 供应商 \_ id**、 **芯片 \_ id hi** 和 **芯片 \_ id lo** 值是否与某个驱动程序的某个缓存副本的配置 rom 内容的标头中的相同值匹配。
2.  如果在步骤1中找到匹配项，则总线驱动程序将确定总线信息块中的生成值是否匹配。 如果代值未更改 (或者设置为1（表示它不会更改) ），则总线驱动程序将重用配置 ROM 的缓存内容。

可以在 IEEE 1394 规范的前面步骤中找到配置 ROM 值的说明。 如果 1394ohci.sys 总线驱动程序找不到匹配的缓存配置 ROM 标头，或者必须重新读取节点配置 ROM 的内容，因为 **生成** 值发生了更改，则将按照前面的步骤来检索新配置 ROM 的内容。

## <a name="related-topics"></a>相关主题
[IEEE 1394 驱动程序堆栈](./the-ieee-1394-driver-stack.md)  
[修改 1394 配置 ROM](./modifying-the-1394-configuration-rom.md)  
[**请求 \_ 获取 \_ 配置 \_ ROM**](https://msdn.microsoft.com/library/windows/hardware/gg266404)
