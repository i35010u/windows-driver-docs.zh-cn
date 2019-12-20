---
title: 数据包描述符和扩展
description: 数据包描述符和扩展
ms.assetid: 7B2357AE-F446-4AE8-A873-E13DF04D8D71
keywords:
- WDF 网络适配器类扩展数据包描述符和扩展，NetAdapterCx 数据路径描述符，多环缓冲区，NetAdapterCx 数据包描述符，NetAdapterCx 数据包扩展
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: c34a3f491f7c16c315c24455bc984f77e9025035
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209034"
---
# <a name="packet-descriptors-and-extensions"></a>数据包描述符和扩展

在 NetAdapterCx 中，*数据包描述符*是用于描述网络数据包的小型、精简、运行时可扩展的结构。 每个数据包都需要以下各项：

- 一个核心描述符 
- 一个或多个片段说明符
- 零个或多个数据包扩展 

数据包的*核心描述符*是[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)结构。 它仅包含适用于所有数据包的最基本的元数据，例如给定包的组帧布局和数据包的第一个段描述符的索引。   

每个数据包还必须有一个或多个*片段描述符*或[**NET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fragment/ns-fragment-_net_fragment)结构，它们描述数据包数据所在的系统内存中的位置。

*扩展名*是可选的，可为特定于方案的功能保留每个数据包或每个片段的元数据。 例如，数据包扩展可以保存校验和的卸载信息、大型发送卸载（LSO）和接收段合并（RSC），也可以保存特定于应用程序的详细信息。 片段扩展可以保存虚拟地址信息、逻辑 DMA 地址信息或片段的其他信息。

这些描述符和扩展共同保存了有关网络数据包的所有元数据。 下面是两个示例，说明了如何描述数据包。 第一张图显示了这样一种情况：整个数据包存储在单个内存片段内，并已启用校验和卸载。

![1片段数据包布局](images/packet_layout_1_extension_1_fragment.png)

第二个图显示存储在两个内存片段中的数据包，同时启用 RSC 和 checksum 卸载。

![2分段数据包布局](images/packet_layout_2_extensions_2_fragments.png)


## <a name="packet-descriptor-storage-and-access"></a>数据包描述符存储和访问

数据包描述符和片段描述符均存储在**NET_RING**结构中。 NIC 客户端驱动程序通过调入网络环迭代器接口来访问网络环并对其执行操作，从而使驱动程序可以使用 NetAdapterCx 将网络数据发布到硬件，并将已完成的数据排出回操作系统。 

有关网络环和 Net 环形迭代器接口的详细信息，请参阅[净环简介](introduction-to-net-rings.md)。

## <a name="packet-descriptor-extensibility"></a>数据包描述符扩展性

扩展性是 NetAdapterCx 数据包描述符的核心功能，形成了描述符的 versionability 和性能的基础。 在运行时，操作系统将为连续块中的每个数据包队列分配所有数据包描述符，同时为所有可用扩展。 每个扩展块紧跟在核心描述符后面，如下图所示：

![NetAdapterCx 数据包描述符布局](images/packet-descriptors-1-layout.png)

不允许 NIC 客户端驱动程序将偏移量硬编码到任何扩展块。 相反，它们必须在运行时查询到任何特定扩展的偏移量。 例如，驱动程序可能会查询扩展 B 的偏移量，并返回70字节，如下图所示：

![查询核心数据包描述符扩展的偏移量](images/packet-descriptors-2-offset-query.png)

一旦创建了数据包队列及其描述符，系统就保证它们的所有扩展偏移都是固定的，因此，驱动程序不必经常重新查询偏移量。 此外，由于在初始化数据包队列时，所有扩展都由系统中的系统预分配，因此，无需对块进行运行时分配，搜索列表中的特定描述符，或者必须存储指向每个数据包的指针拓.

## <a name="packet-descriptor-versionability"></a>数据包描述符 versionability

在未来的版本中，可以通过将新字段添加到末尾来轻松扩展 NetAdapterCx 的核心数据包描述符，如下图所示：

![NetAdapterCx 核心数据包描述符版本控制](images/packet-descriptors-3-core-descriptor-versioning.png)

了解 V2 字段的更高版本的客户端驱动程序可以访问它们，而较早的基于 V1 的驱动程序将使用扩展偏移来跳过 V2 字段，以便它们可以访问其理解的字段。 此外，还可以通过相同的方式对每个扩展进行版本控制，如下图所示：

![NetAdapterCx 数据包扩展版本控制](images/packet-descriptors-4-extension-versioning.png)

了解新扩展的客户端驱动程序可以使用它。 其他客户端驱动程序可以跳过新字段。 这允许单独对数据包描述符的不同部分进行版本控制。

## <a name="packet-descriptors-and-datapath-performance"></a>数据包描述符和数据路径性能

前面概述的扩展性功能可帮助客户端驱动程序满足每秒 capabable 的 Nic 的性能要求，以及数千个队列：

1. 由于不使用的功能和扩展会在描述符中占用0字节的空间，因此数据包描述符尽可能压缩，以改善 CPU 缓存命中。 
2. 没有指针取消引用，因此只有偏移算法，因为扩展插件为内联，这不仅节省空间，还有助于 CPU 缓存命中。 
3. 在创建队列时将分配扩展，因此驱动程序无需在活动数据路径中分配和释放内存，也无需处理后备链表的上下文块列表。

## <a name="using-packet-extensions"></a>使用包扩展 

> [!IMPORTANT]
> 目前，客户端驱动程序仅限于[操作系统定义的预先存在的数据包扩展](#predefined-packet-extension-constants-and-helper-methods)。

### <a name="registering-packet-extensions"></a>正在注册包扩展

使用 NIC 客户端驱动程序中的数据包扩展的第一步是声明受支持的硬件卸载。 当你播发对卸载（如校验和和 LSO）的支持时，NetAdapterCx 会以你的名义自动注册关联的数据包扩展。

有关为校验和和 LSO 公布硬件卸载的代码示例，请参阅[NetAdapterCx 硬件卸载](netadaptercx-hardware-offloads.md)。

### <a name="querying-packet-extension-offsets-for-datapath-queues"></a>查询数据路径队列的数据包扩展偏移量

通过声明硬件卸载支持来注册数据包扩展后，在处理数据包时，需要使用扩展偏移量来访问每个包。 若要减少对驱动程序的调用并提高性能，可以在*EvtNetAdapterCreateTx （Rx）队列*回调函数期间查询扩展的偏移量，并将偏移信息存储在队列上下文中。 

有关查询扩展偏移并将其存储在队列上下文中的示例，请参阅[传输和接收队列](transmit-and-receive-queues.md)。

### <a name="getting-packet-extensions-at-runtime"></a>在运行时获取数据包扩展

在队列上下文中存储了扩展偏移量后，只要需要扩展中的信息，就可以使用它们。 例如，你可以在将描述符编程到传输队列的硬件时调用[**NetExtensionGetPacketChecksum**](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksum/nf-checksum-netextensiongetpacketchecksum)方法：

```C++
    // Get the extension offset from the device context
    PMY_TX_QUEUE_CONTEXT queueContext = GetMyTxQueueContext(txQueue);
    NET_EXTENSION checksumExtension = queueContext->ChecksumExtension;

    // Get the checksum info for this packet
    NET_PACKET_CHECKSUM* checksumInfo = NetExtensionGetPacketChecksum(checksumExtension, packetIndex);

    // Do work with the checksum info
    if (packet->Layout.Layer3Type == NET_PACKET_LAYER3_TYPE_IPV4_NO_OPTIONS ||
        packet->Layout.Layer3Type == NET_PACKET_LAYER3_TYPE_IPV4_WITH_OPTIONS ||
        packet->Layout.Layer3Type == NET_PACKET_LAYER3_TYPE_IPV4_UNSPECIFIED_OPTIONS)
    {
        if(checksumInfo->Layer4 == NET_PACKET_TX_CHECKSUM_REQUIRED)
        {
            ...
        }
    }
    ...
```

## <a name="predefined-packet-extension-constants-and-helper-methods"></a>预定义的数据包扩展常量和帮助器方法

NetAdapterCx 提供已知包扩展常量的定义。

| Constant | 定义 |
| --- | --- |
| NET_PACKET_EXTENSION_INVALID_OFFSET | 防止偏移大小无效。 |
| <ul><li>NET_PACKET_EXTENSION_CHECKSUM_NAME</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1_SIZE</li></ul> | 校验和数据包扩展的名称、版本和大小。 |
| <ul><li>NET_PACKET_EXTENSION_LSO_NAME</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1_SIZE</li></ul> | 大型发送卸载（LSO）数据包扩展的名称、版本和大小。 |
| <ul><li>NET_PACKET_EXTENSION_RSC_NAME</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1_SIZE</li></ul> | 接收段合并（RSC）数据包扩展的名称、版本和大小。 |

此外，NetAdapterCx 还提供了三种帮助器方法，它们充当[**NetExtensionGetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extension/nf-extension-netextensiongetdata)方法的包装器。 其中每个方法都返回指向适当结构类型的指针。

| 方法 | 结构 |
| --- | --- |
| [**NetExtensionGetPacketChecksum**](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksum/nf-checksum-netextensiongetpacketchecksum) | [**NET_PACKET_CHECKSUM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksumtypes/ns-checksumtypes-_net_packet_checksum) |
| [**NetExtensionGetLso**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lso/nf-lso-netextensiongetpacketlso) | [**NET_PACKET_LSO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lsotypes/ns-lsotypes-_net_packet_lso)
| [**NetExtensionGetPacketRsc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsc/nf-rsc-netextensiongetpacketrsc) | [**NET_PACKET_RSC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsctypes/ns-rsctypes-_net_packet_rsc) |
