---
title: RSS 配置
description: RSS 配置
ms.assetid: 84a00163-6908-439a-a980-c13f0ec8e3c1
keywords:
- 接收方缩放 WDK 网络，ndirection 表示例
- RSS WDK 网络，间接表示例
- 接收方缩放 WDK 网络，配置
- RSS WDK 网络，配置
- ndirection 表示例 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db0a3be2ed1e3c171e7f8c5ba4672fe44b507954
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211605"
---
# <a name="rss-configuration"></a>RSS 配置





为获取 RSS 配置信息，过量驱动程序可以将 [oid 生成 \_ \_ 接收 \_ 缩放 \_ 功能](./oid-gen-receive-scale-capabilities.md) 的 oid 查询发送到微型端口驱动程序。 在初始化期间，NDIS 还向 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构中的过量协议驱动程序提供 RSS 配置信息。

过量驱动程序选择哈希函数、类型和间接寻址表。 若要设置这些配置选项，驱动程序将向微型端口驱动程序发送 oid 请求，即 [oid 生成 \_ \_ 接收 \_ 缩放 \_ 参数](./oid-gen-receive-scale-parameters.md) 。 过量驱动程序还可以查询此 OID 以获取当前 RSS 设置。 OID \_ GEN \_ 接收 \_ 缩放参数 OID 的信息缓冲区 \_ 包含指向 [**NDIS \_ 接收 \_ 缩放 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters) 结构的指针。

过量驱动程序可以在 NIC 上禁用 RSS。 在这种情况下，驱动程序 \_ 会在 \_ \_ \_ \_ ndis **Flags** \_ 接收 \_ 缩放参数结构的 Flags 成员中设置 ndis rss 参数标志 "禁用 RSS" 标志 \_ 。 设置此标志后，微型端口驱动程序应忽略所有其他标志和设置并在 NIC 上禁用 RSS。

NDIS 首先处理 OID 生成 \_ \_ 接收 \_ 缩放 \_ 参数，然后将其传递给微型端口驱动程序，然后更新微型端口适配器的 \* RSS 标准化关键字（如果需要）。 有关** \* rss**关键字的详细信息，请参阅[Rss 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)。

接收到 [OID 生成 \_ \_ 接收 \_ 刻度 \_ 参数](./oid-gen-receive-scale-parameters.md) set 请求并在 NDIS \_ RSS 参数标志的情况 \_ \_ \_ 下禁用 \_ RSS 标志后，微型端口驱动程序应在初始化后将 nic 的 RSS 状态设置为 nic 的初始状态。 因此，如果微型端口驱动程序接收到后一代 OID 生成 \_ \_ 接收 \_ 刻度 \_ 参数，并在 NDIS \_ rss \_ 参数 \_ 标志 \_ 中清除了 "禁用 \_ RSS 标志"，则所有参数的值都应与在小型 \_ \_ \_ \_ 端口适配器初始化后首次收到 OID 生成接收缩放参数 set 请求后设置的值相同。

过量驱动程序可以使用 [OID 生成 \_ \_ 接收 \_ 哈希](./oid-gen-receive-hash.md) OID 在收到的帧上启用和配置哈希计算，而无需启用 RSS。 过量驱动程序还可以查询此 OID 以获取当前的接收哈希设置。

OID 生成 \_ \_ 接收 \_ 哈希 oid 的信息缓冲区包含指向 [**NDIS \_ 接收 \_ 哈希 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters) 结构的指针。 对于集请求，OID 指定微型端口适配器应使用的哈希参数。 对于查询请求，OID 返回微型端口适配器使用的哈希参数。 此 OID 对于支持 RSS 的驱动程序是可选的。

**注意**   如果启用了接收哈希计算，NDIS 会在启用 RSS 之前禁用接收哈希计算。 如果启用了 RSS，NDIS 会在启用接收哈希计算之前禁用 RSS。

 

微型端口驱动程序支持的所有微型端口适配器必须为所有后续协议绑定提供相同的哈希配置设置。 此 OID 还包括一个密钥，小型端口驱动程序或 NIC 必须使用该密钥进行哈希计算。 密钥的长度为320位 (40 字节) ，可以包含过量驱动程序选择的任何数据，例如，随机字节流。

为了重新平衡处理负载，过量驱动程序可以设置 RSS 参数并修改间接寻址表。 通常，除间接表外，所有参数都保持不变。 但是，初始化 RSS 后，上层驱动程序可能会更改其他 RSS 初始化参数。 如果需要，微型端口驱动程序可以重置 NIC 硬件，以更改哈希函数、哈希机密密钥、哈希类型、基本 CPU 号或用于为间接寻址建立索引的位数。

**注意**   过量驱动程序可以随时设置这些参数。 这可能导致不按顺序接收指示。 支持 TCP 的微型端口驱动程序无需在此实例中清除其接收队列。

 

下图提供了间接寻址表的两个实例的示例内容。

![阐释 rss 间接寻址表的两个实例的内容的关系图](images/rss-table.png)

上图假设有四个处理器配置，并且哈希值中使用的最小有效位数为6位。 因此，间接寻址表中包含64个条目。

在此图中，表 A 在初始化后立即列出间接寻址表中的值。 以后，当正常流量负载变化时，处理器负载会增长不均衡。 过量驱动程序检测到不平衡的情况，并通过定义新的间接表尝试重新平衡负载。 表 B 列出了新的间接寻址表值。 在表 B 中，CPU 2 的某些负载会移至 Cpu 1 和3。

**注意**   当间接寻址表发生更改时，如果在) 中处理当前的接收描述符队列，则会在出现错误的 CPU 上处理 (。 这是正常的暂时性情况。

 

间接寻址表的大小通常是系统中处理器数的两倍到八倍。

当微型端口驱动程序将数据包分发到 Cpu 时，如果 Cpu 太多，则在分发负载时所用的工作量可能会变得不受制约。 在这种情况下，过量驱动程序应选择对网络数据进行处理的 Cpu 子集。

在某些情况下，可用的硬件接收队列数可能小于系统上的 Cpu 数。 微型端口驱动程序必须检查间接表以确定要与硬件队列关联的 CPU 号。 如果间接寻址表中出现的不同 CPU 号总数大于 NIC 支持的硬件队列数，则微型端口驱动程序必须从间接表中选取一部分 CPU 号。 子集的数量等于硬件队列的数量。 微型端口驱动程序从 OID 生成 **IndirectionTableSize** 参数获取了该参数 [ \_ \_ \_ \_ ](./oid-gen-receive-scale-parameters.md)。 微型端口驱动程序指定 **NumberOfReceiveQueues** 值以响应 OID 生成 \_ \_ 接收 \_ 缩放 \_ 功能。

 

