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
ms.openlocfilehash: 8cdfd45a7f93baef9b0f5d933c85340ed8dfea42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842012"
---
# <a name="rss-configuration"></a>RSS 配置





为了获取 RSS 配置信息，过量驱动程序可以将 Oid 的 OID 查询发送[\_代\_接收\_将\_功能缩放](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-capabilities)到微型端口驱动程序。 NDIS 还在初始化期间[ **\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构，在 ndis 中向过量协议驱动程序提供 RSS 配置信息。

过量驱动程序选择哈希函数、类型和间接寻址表。 若要设置这些配置选项，驱动程序将[\_GEN\_接收\_将\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-parameters)发送到微型端口驱动程序来发送 OID 的 oid 设置请求。 过量驱动程序还可以查询此 OID 以获取当前 RSS 设置。 OID\_GEN\_接收\_规模的信息缓冲区\_参数 OID 包含一个指向[**NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)\_\_个参数结构的指针。

过量驱动程序可以在 NIC 上禁用 RSS。 在这种情况下，驱动程序将 NDIS\_RSS\_PARAM 设置\_标志\_在 NDIS\_接收\_的**标志**成员\_参数结构中禁用\_RSS 标志。 设置此标志后，微型端口驱动程序应忽略所有其他标志和设置并在 NIC 上禁用 RSS。

NDIS 处理 OID\_GEN\_在将其传递给微型端口驱动程序之前接收\_缩放\_参数，并根据需要更新微型端口适配器的 \*RSS 标准化关键字。 有关 **\*rss**关键字的详细信息，请参阅[RSS 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)。

接收 OID 后[\_代\_接收\_比例\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-parameters)使用 NDIS\_rss 设置请求\_参数\_，微型端口驱动程序应在初始化后将 NIC 的 RSS 状态设置为 NIC 的初始状态。 因此，如果微型端口驱动程序收到后续 OID\_代\_接收\_缩放\_参数使用 NDIS\_RSS\_参数设置请求\_，所有参数的值都应与微型端口驱动程序收到 OID 后设置的值相同，\_第一次\_接收\_\_缩放。

过量驱动程序可以使用[OID\_GEN\_接收\_哈希](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-hash)OID）在收到的帧上启用和配置哈希计算，而无需启用 RSS。 过量驱动程序还可以查询此 OID 以获取当前的接收哈希设置。

OID\_GEN\_接收\_哈希 OID 的信息缓冲区包含指向[**NDIS\_接收\_哈希\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)结构的指针。 对于集请求，OID 指定微型端口适配器应使用的哈希参数。 对于查询请求，OID 返回微型端口适配器使用的哈希参数。 此 OID 对于支持 RSS 的驱动程序是可选的。

**请注意**  如果启用了接收哈希计算，NDIS 将在启用 RSS 之前禁用接收哈希计算。 如果启用了 RSS，NDIS 会在启用接收哈希计算之前禁用 RSS。

 

微型端口驱动程序支持的所有微型端口适配器必须为所有后续协议绑定提供相同的哈希配置设置。 此 OID 还包括一个密钥，小型端口驱动程序或 NIC 必须使用该密钥进行哈希计算。 密钥的长度为320位长（40个字节），可以包含过量驱动程序选择的任何数据，例如，随机字节流。

为了重新平衡处理负载，过量驱动程序可以设置 RSS 参数并修改间接寻址表。 通常，除间接表外，所有参数都保持不变。 但是，初始化 RSS 后，上层驱动程序可能会更改其他 RSS 初始化参数。 如果需要，微型端口驱动程序可以重置 NIC 硬件，以更改哈希函数、哈希机密密钥、哈希类型、基本 CPU 号或用于为间接寻址建立索引的位数。

**请注意**  过量驱动程序可以随时设置这些参数。 这可能导致不按顺序接收指示。 支持 TCP 的微型端口驱动程序无需在此实例中清除其接收队列。

 

下图提供了间接寻址表的两个实例的示例内容。

![阐释 rss 间接寻址表的两个实例的内容的关系图](images/rss-table.png)

上图假设有四个处理器配置，并且哈希值中使用的最小有效位数为6位。 因此，间接寻址表中包含64个条目。

在此图中，表 A 在初始化后立即列出间接寻址表中的值。 以后，当正常流量负载变化时，处理器负载会增长不均衡。 过量驱动程序检测到不平衡的情况，并通过定义新的间接表尝试重新平衡负载。 表 B 列出了新的间接寻址表值。 在表 B 中，CPU 2 的某些负载会移至 Cpu 1 和3。

**请注意**  更改了间接寻址表后，一小段时间（正在处理当前的接收描述符队列），可以在错误的 CPU 上处理包。 这是正常的暂时性情况。

 

间接寻址表的大小通常是系统中处理器数的两倍到八倍。

当微型端口驱动程序将数据包分发到 Cpu 时，如果 Cpu 太多，则在分发负载时所用的工作量可能会变得不受制约。 在这种情况下，过量驱动程序应选择对网络数据进行处理的 Cpu 子集。

在某些情况下，可用的硬件接收队列数可能小于系统上的 Cpu 数。 微型端口驱动程序必须检查间接表以确定要与硬件队列关联的 CPU 号。 如果间接寻址表中出现的不同 CPU 号总数大于 NIC 支持的硬件队列数，则微型端口驱动程序必须从间接表中选取一部分 CPU 号。 子集的数量等于硬件队列的数量。 微型端口驱动程序从 OID 获取了**IndirectionTableSize**参数[\_GEN\_接收\_缩放\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-parameters)。 微型端口驱动程序指定**NumberOfReceiveQueues**值以响应 OID\_GEN\_接收\_缩放\_功能。

 

 





