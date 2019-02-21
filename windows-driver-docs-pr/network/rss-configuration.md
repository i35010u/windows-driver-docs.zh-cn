---
title: RSS 配置
description: RSS 配置
ms.assetid: 84a00163-6908-439a-a980-c13f0ec8e3c1
keywords:
- 接收方缩放 WDK 网络，ndirection 表示例
- RSS WDK 网络，间接表示例
- 接收方缩放 WDK 网络、 配置
- RSS WDK 网络、 配置
- ndirection 表示例 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf8b8b30a3b5ffb52e5c274f61f636140091218e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521394"
---
# <a name="rss-configuration"></a>RSS 配置





若要获取 RSS 配置信息，基础驱动程序可以发送的 OID 查询[OID\_代\_接收\_规模\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569636)微型端口驱动程序。 NDIS 还提供了到过量协议中的驱动程序的 RSS 配置信息[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)在初始化过程中的结构。

基础驱动程序将选择哈希函数、 类型和间接表。 若要设置这些配置选项，该驱动程序发送的 OID 集请求[OID\_代\_接收\_规模\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569637)微型端口驱动程序。 过量驱动程序还可以查询此 OID 以获得当前的 RSS 设置。 OID 信息缓冲区\_GEN\_接收\_规模\_参数 OID 包含一个指向[ **NDIS\_接收\_规模\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567228)结构。

基础驱动程序可以禁用 RSS nic 在这种情况下，驱动程序设置 NDIS\_RSS\_PARAM\_标志\_禁用\_RSS 标志中**标志**成员 NDIS\_接收\_规模\_参数结构。 微型端口驱动程序时设置此标志，应忽略所有其他标志和设置并禁用 RSS nic

NDIS 处理 OID\_GEN\_接收\_规模\_参数，然后再将它传递到微型端口驱动程序和更新的微型端口适配器\*RSS 标准化关键字，如果所需。 有关详细信息 **\*RSS**关键字，请参阅[RSS 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)。

收到后[OID\_代\_接收\_规模\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569637)集请求与的 NDIS\_RSS\_PARAM\_标志\_禁用\_RSS 标志设置，在初始化之后，微型端口驱动程序应将 NIC RSS 状态设置为 NIC 的初始状态。 因此，如果微型端口驱动程序收到的后续 OID\_GEN\_接收\_规模\_参数设置请求与的 NDIS\_RSS\_PARAM\_标志\_禁用\_RSS 清除标志，所有参数应具有相同的值后微型端口驱动程序收到 OID 设置的\_常规\_接收\_规模\_第一次的微型端口适配器已初始化后，设置请求参数。

基础驱动程序可以使用[OID\_代\_接收\_哈希](https://msdn.microsoft.com/library/windows/hardware/ff569635)OID 来启用和配置上的哈希计算接收帧，而不启用 RSS。 过量驱动程序还可以查询以获得当前接收哈希设置此 OID。

OID 信息缓冲区\_GEN\_接收\_哈希 OID 包含一个指向[ **NDIS\_接收\_哈希\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567190)结构。 对于组的请求，OID 指定微型端口适配器应使用的哈希参数。 对于查询请求，OID 返回微型端口适配器使用的哈希参数。 此 OID 是可选的支持 RSS 的驱动程序。

**请注意**  如果接收哈希计算已启用、 NDIS 禁用接收哈希计算之前启用了 RSS。 如果启用了 RSS，NDIS 禁用 RSS 之前它使接收哈希计算。

 

所有微型端口驱动程序支持的微型端口适配器必须提供相同的哈希到所有后续协议绑定的配置设置。 此 OID 还包括微型端口驱动程序或 NIC 必须使用的哈希计算的机密密钥。 该密钥为 320 位长 （40 个字节），并且可以包含基础驱动程序选择，例如，随机字节流的任何数据。

若要重新平衡的处理负载，基础驱动程序可以设置 RSS 参数并修改间接表。 通常情况下，所有参数都是不变的间接寻址表除外。 但是，RSS 在初始化后，基础驱动程序可能会更改其他 RSS 初始化参数。 如有必要，微型端口驱动程序可以重置 NIC 硬件更改哈希函数、 哈希密钥、 哈希类型、 基本的 CPU 数或用于间接表编制索引的比特数。

**请注意**  基础驱动程序可以随时设置这些参数。 这可能会导致不按顺序接收的指示。 支持 TCP 的微型端口驱动程序不需要清除其接收队列在这种情况。

 

下图提供了两个实例的间接寻址表的示例内容。

![说明 rss 间接表的两个实例的内容的关系图](images/rss-table.png)

上图假定的四个处理器配置，和的哈希值中使用的最低有效位数为 6 位。 因此，间接表包含 64 个项目。

在图中，表 A 初始化后立即列出间接表中的值。 更高版本，随着正常流量负荷变化，处理器负荷增加不平衡。 基础驱动程序检测到不均衡的情况，并尝试通过定义新的间接寻址表重新平衡负载。 表 B 列出了新的间接寻址表值。 在表 B 中，一些 CPU 2 中的负载会移动到 Cpu 1 和 3。

**请注意**  间接表更改时，在短时间 （在当前接收要处理队列的描述符） 时，可以上错误的 CPU 处理数据包。 这是正常的暂时性情况。

 

间接寻址表的大小通常是在系统中处理器数量的二到八倍。

当微型端口驱动程序将分发到的 Cpu 和数据包，如果有太多 Cpu 时，花费的时间中分散负载可能令人望而却步。 在这种情况下，过量驱动程序应选择网络数据的处理出现的 Cpu 的子集。

在某些情况下，接收队列执行的可用硬件数可能小于在系统上的 Cpu 数。 微型端口驱动程序必须检查间接表来确定 CPU 编号，以将与硬件队列相关联。 如果多个 NIC 支持的硬件队列数目的间接寻址表中显示的不同 CPU 数量总数，微型端口驱动程序必须选择间接表中的 CPU 数的子集。 硬件队列数数等于子集。 获取该微型端口驱动程序**IndirectionTableSize**中的参数[OID\_常规\_接收\_规模\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569637)。 指定的微型端口驱动程序**NumberOfReceiveQueues**值以响应 OID\_常规\_接收\_规模\_功能。

 

 





