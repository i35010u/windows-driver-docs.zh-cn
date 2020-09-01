---
title: NDIS 虚拟机 (VM) 共享内存的安全问题
description: NDIS 虚拟机 (VM) 共享内存的安全问题
ms.assetid: 42b903b0-6729-4314-9305-9345fff9b2ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e2924e89a9a8e055500dd7b39a4c4371b91eba4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210081"
---
# <a name="security-issues-with-ndis-virtual-machine-vm-shared-memory"></a>NDIS 虚拟机 (VM) 共享内存的安全问题





本主题讨论从虚拟机 (VM) 为虚拟机队列 (VMQ) 接收缓冲区分配共享内存所涉及的潜在安全问题。 本主题包含以下各节：

-   [VM 共享内存的安全问题概述](#overview)

-   [Windows Server 2008 R2 如何解决安全问题](#ndis620)

-   [Windows Server 2012 和更高版本如何解决安全问题](#ndis630)

**注意**   在 Hyper-v 中，子分区也称为 VM。

 

### <a name="overview-of-the-security-issues-with-vm-shared-memory"></a><a href="" id="overview"></a>VM 共享内存的安全问题概述

Vm 不是受信任的软件实体。 也就是说，恶意 VM 不得干扰其他 Vm，也不能干扰 Hyper-v 父分区中运行的管理操作系统。 本部分提供了背景信息和要求，以确保驱动程序编写人员了解 VMQ 安全问题和共享内存的要求。 有关共享内存的详细信息，请参阅 "[编写 VMQ 驱动程序](writing-vmq-drivers.md)" 部分中的 "[共享内存资源分配](shared-memory-resource-allocation.md)" 主题。

在虚拟化环境中，vm 共享内存可以通过 VM 来查看或修改。 但是，不允许查看或修改与其他 Vm 关联的数据。 还不允许 Vm 访问管理操作地址空间。

所接收数据包的标头部分必须受到保护。 不允许 VM 影响网络虚拟服务提供商 (VSP) 中的 Hyper-v 可扩展交换机的行为。 因此，必须先执行 VLAN (虚拟 LAN) 筛选，然后网络适配器才能使用 DMA 将数据传输到 VM 共享内存。 此外， (MAC) 地址学习的媒体访问控制不会受到影响。

如果连接到 VM 的 Hyper-v 可扩展交换机端口具有关联的 VLAN 标识符，则在主机将数据包转发到 VM 的虚拟网络适配器之前，主计算机必须确保传入帧的目标 MAC 地址和 VLAN 标识符与端口的相应属性匹配。 如果帧的 VLAN 标识符与端口的 VLAN 标识符不匹配，则会丢弃数据包。 当从主机内存中分配虚拟网络适配器的接收缓冲区时，主机可以检查 VLAN 标识符，并在必要时删除该帧，然后使该帧的内容对目标 VM 可见。 如果未将帧复制到 VM 的地址空间，该 VM 将无法访问它。

但是，当 VMQ 配置为使用共享内存时，网络适配器将使用 DMA 将传入帧直接传输到 VM 地址空间。 此传输引入了一个安全问题，在这种情况下，VM 可以检查接收到的帧的内容，而无需等待可扩展交换机应用所需的 VLAN 筛选。

### <a name="how-windows-server2008r2-addresses-the-security-issue"></a><a href="" id="ndis620"></a>Windows Server 2008 R2 如何解决安全问题

在 Windows Server 2008 R2 中，在 VSP 将 VM 队列配置为使用从 VM 地址空间分配的共享内存之前，它对队列使用以下筛选测试。

```syntax
(MAC address == x) && (VLAN identifier == n)
```

如果网络适配器硬件可以在 DMA 传输到接收缓冲区之前支持此测试，网络适配器可以丢弃具有无效 VLAN 标识符的帧，或将其发送到默认队列，以便可扩展交换机可以对其进行筛选。 如果微型端口驱动程序成功请求在队列中设置具有此测试的筛选器，则可扩展交换机可以为该队列使用 VM 共享内存。 但是，如果网络适配器硬件不能基于目标 MAC 地址和 VLAN 标识符筛选帧，则可扩展交换机为该队列使用主机共享内存。

可扩展交换机会检查接收帧的源 MAC 地址，以配置传输帧的路由信息，也就是说，它类似于物理学习交换机。 可以在主机堆栈中安装防火墙筛选器驱动程序;例如，在网络适配器硬件的微型端口驱动程序上，在可扩展交换机驱动程序的下面。 防火墙筛选器驱动程序可以在可扩展交换机之前访问接收的帧中的数据。 如果每个帧的整个接收缓冲区都是从 VM 地址空间分配的，则恶意 VM 可以访问该主机中运行的筛选器驱动程序或可扩展交换机要检查的帧部分。

若要解决此安全问题，请在为 VM 队列使用 VM 共享内存时，网络适配器必须将数据包拆分为至少为预测先行大小（预先确定的固定值）的字节偏移量。 任何预测先行数据（意味着在预测先行大小之前的字节偏移量之前的数据）必须与为预测先行数据分配的共享内存一起传输。 后先行预测数据（帧有效负载的其余部分）应该与为后续预测后数据分配的共享内存一起传输。

下图显示了在将传入数据拆分为预测先行和后期预测共享内存缓冲区时网络数据结构的关系。

![说明包含预测先行和后期预测数据的 vmq 数据包结构的关系图](images/vmqpacket.png)

VMQ 共享内存的摘要要求如下所示：

-   网络适配器可以将接收的帧拆分为大于预测先行大小的网络标头边界。 但是，当由 NDIS 请求且没有异常时，接收并分配到 VMQ 的所有帧都必须拆分为或超出 NDIS 请求的预测先行大小边界。

-   必须使用 DMA 将预测先行数据与微型端口驱动程序分配的共享内存传输。 微型端口驱动程序必须在分配调用中指定内存将用于预测数据的。

-   必须使用 DMA 将后续预测后数据传输到由微型端口驱动程序分配的共享内存。 微型端口驱动程序必须在分配调用中指定内存将用于后续预测后的数据。

-   微型端口驱动程序不得依赖于 NDIS 将用来完成共享内存分配请求的地址空间。 也就是说，用于预测先行或后预测数据的共享内存地址空间是特定于实现的。 在许多情况下，NDIS 或可扩展交换机可能满足所有请求，包括来自主机内存地址空间的用于后先行使用的请求。

-   当该队列中的帧显示在驱动程序堆栈上时，必须保留对 VMQ 接收队列接收帧的顺序。

-   网络适配器必须在每个后期预测缓冲区中分配足够的回填内存空间。 此分配允许将预测先行数据复制到后期预测后缓冲区的回填部分，并允许将帧传递到连续缓冲区中的 VM。

如果硬件中没有用于满足对 VMQ 共享内存的要求的机制，则在接收端支持分散收集 DMA 的硬件可能会通过为每个接收的帧分配两个接收缓冲区来实现相同的结果。 在这种情况下，第一个缓冲区的大小限制为请求的预测先行大小。

如果网络适配器无法通过任何方法满足对 VMQ 共享内存的这些要求，则该 VSP 将从主机地址空间为 VMQ 接收缓冲区分配内存，并将接收的数据包从网络适配器接收缓冲区复制到 VM 地址空间。

### <a name="how-windows-server2012-and-later-versions-address-the-security-issue"></a><a href="" id="ndis630"></a>Windows Server 2012 和更高版本如何解决安全问题

从 Windows Server 2012 开始，VSP 不会为 VMQ 接收缓冲区从 VM 分配共享内存。 相反，VSP 从主机地址空间为 VMQ 接收缓冲区分配内存，然后将接收的数据包从网络适配器接收缓冲区复制到 VM 地址空间。

以下几点适用于在 Windows Server 2012 和更高版本的 Windows 上运行的 VMQ 微型端口驱动程序：

-   对于 NDIS 6.20 VMQ 微型端口驱动程序，无需更改。 但是，当 VSP 通过发出 OID (对象标识符) 方法请求来分配一个 VM 队列时，该请求会将[**NDIS 接收 \_ \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的**LookaheadSize**成员设置为零。 [ \_ \_ \_ \_ ](./oid-receive-filter-allocate-queue.md) 这会强制微型端口驱动程序不会将数据包拆分为预先预测前和预测后缓冲区。

-   从 NDIS 6.30 开始，VMQ 微型端口驱动程序不得公布对将数据包数据拆分为预先预测和后先行缓冲区的支持。 当微型端口驱动程序注册其 VMQ 功能时，它必须在初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构时遵循以下规则：

    -   微型端口驱动程序不得在**Flags**成员中设置**NDIS \_ 接收 \_ 筛选器 \_ 预测先行 \_ 拆分 \_ 支持**标志。

    -   微型端口驱动程序必须将 **MinLookaheadSplitSize** 和 **MaxLookaheadSplitSize** 成员设置为零。

    有关如何注册 VMQ 功能的详细信息，请参阅 [确定网络适配器的 Vmq 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

 

