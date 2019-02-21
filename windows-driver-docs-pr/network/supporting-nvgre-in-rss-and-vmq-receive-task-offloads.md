---
title: 支持 NVGRE 在 RSS 和 VMQ 接收任务卸载
description: 本部分介绍支持 NVGRE RSS 和 VMQ 接收任务卸载
ms.assetid: 42660D55-31C0-4101-9EA1-159EBB76B019
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f0bf5311665b7a7a362b314d28ebe698f2c0dc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534510"
---
# <a name="supporting-nvgre-in-rss-and-vmq-receive-task-offloads"></a>支持 NVGRE 在 RSS 和 VMQ 接收任务卸载


NDIS 6.30 (Windows Server 2012) 引入了[网络虚拟化使用通用路由封装 (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 NDIS 微型端口驱动程序和 Nic，可以执行[接收方伸缩](receive-scaling.md)(RSS) 和[虚拟机队列 (VMQ)](virtual-machine-queue--vmq-.md)接收卸载应执行此操作的方式支持 NVGRE 的任务。

**请注意**  此页面假定您熟悉中的信息[卸载分段的大型 TCP 数据包](offloading-the-segmentation-of-large-tcp-packets.md)。

 

如果微型端口驱动程序支持 RSS 和 VMQ 封装的数据包，它必须播发中的这些功能**RssSupported**并**VmqSupported**的成员[ **NDIS\_封装\_数据包\_任务\_卸载**](https://msdn.microsoft.com/library/windows/hardware/jj991956)结构。 如果微型端口公布这些功能，接收[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)OID 请求和成功 OID，NIC 必须执行 RSS 和 VMQ 上播发封装的数据类型。

对于支持封装的数据包，它能分析，NIC 必须在内部 MAC 标头上的传输 （内部） 的 IP 标头和 VMQ 负载中的 TCP 或 UDP 标头上执行 RSS。

用于执行 RSS 和 VMQ，NIC 必须获取到封装的数据包的传输 （内部联接） IP 标头中所述[查找有关封装的数据包，接收路径中的传输标头](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)并检查协议号。 如果 NIC 会收到的数据包，使用一种协议，NIC 可以分析，则应 NIC:

-   执行 RSS 进行传输 （内部联接） IP 标头和 TCP 或 UDP 标头上的 4 元组哈希。
    -   对于封装的数据包微型端口不能分析其协议，NIC 应当对隧道 （外部） IP 标头中的源和目标地址字段执行 2 元组哈希。
    -   对于封装的数据包不包含紧跟在传输 （内部联接） IP 标头的 TCP 或 UDP 标头，NIC 应当对隧道 （外部） IP 标头中的源和目标地址字段执行 2 元组哈希。
-   使用以太网标头中封装的数据执行 VMQ。 对于封装的数据包不包含以太网标头 （内封装的数据），应使用的最外面的以太网标头执行 VMQ。

 

 





