---
title: 数据包描述符和扩展
description: 数据包描述符和扩展
ms.assetid: 7B2357AE-F446-4AE8-A873-E13DF04D8D71
keywords:
- WDF 网络适配器类扩展数据包描述符和扩展，NetAdapterCx 数据路径描述符多环形缓冲区、 NetAdapterCx 数据包描述符、 NetAdapterCx 数据包扩展
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 250eaa4e0c5e6657a04d61f57b59f0c739d7429d
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903479"
---
# <a name="packet-descriptors-and-extensions"></a>数据包描述符和扩展

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

在 NetAdapterCx，*数据包描述符*是小型、 compact、 运行时可扩展描述网络数据包的结构。 每个数据包的要求如下：

- 一个核心描述符 
- 一个或多个片段描述符
- 零个或多个数据包扩展 

*核心描述符*数据包的是[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)结构。 它只包含最基本元数据适用于所有数据包，如给定的数据包和数据包的第一个片段描述符到的索引的组帧布局。   

每个数据包还必须具有一个或多个*片段描述符*，或[ **NET_PACKET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)结构，描述系统内存中的位置，该数据包数据驻留。

*数据包扩展*是可选的包含特定于方案的功能的每个数据包元数据。 例如，扩展可以保存的校验和，大量发送卸载 (LSO) 的卸载信息并接收段合并 (RSC)，或者也可以保存特定于应用程序的详细信息。

在一起，这些描述符和扩展具有网络数据包相关的所有元数据。 以下是它们如何描述数据包的两个示例。 第一个图显示了已开启了整个数据包存储在一个内存段和校验和卸载的方案。

![1 片段数据包布局](images/packet_layout_1_extension_1_fragment.png)

第二个图显示了存储在两个内存片段，使用这两个 RSC 的数据包和校验和卸载已启用。

![2 个片段数据包布局](images/packet_layout_2_extensions_2_fragments.png)


## <a name="packet-descriptor-storage-and-access"></a>数据包描述符存储和访问

数据包描述符和片段描述符都存储在**NET_RING**结构。 NIC 客户端驱动程序访问 net 环，并执行这些操作通过调入 Net 的环迭代器接口，这使驱动程序以使用 NetAdapterCx 网络将数据发送到硬件并释放回操作系统已完成的数据。 

Net 环和网络接口的环迭代器的详细信息，请参阅[Net 环和 net 环迭代器](net-rings-and-net-ring-iterators.md)。

## <a name="packet-descriptor-extensibility"></a>数据包描述符可扩展性

可扩展性是 NetAdapterCx 数据包描述符，从而形成的描述符 versionability 和性能的基础的核心功能。 在运行时，操作系统会数据包的所有描述符都分配每个数据包中的队列的连续块，以及任何可用扩展。 每个扩展块背后的核心描述符，将立即下, 图中所示：

![NetAdapterCx 数据包描述符布局](images/packet-descriptors-1-layout.png)

NIC 客户端驱动程序不允许进行硬编码到任何扩展块的偏移量。 相反，它们必须查询在运行时为任何特定的扩展到的偏移量。 例如，驱动程序可能查询到扩展 B 的偏移量，并在下图中取回等 70 个字节：

![查询到核心数据包描述符的扩展的偏移量](images/packet-descriptors-2-offset-query.png)

一旦创建了数据包队列和其描述符，它们的所有扩展偏移量都保证由系统是恒定的因此驱动程序无需重新查询通常偏移量。 此外，因为在初始化数据包队列的时间中，所有扩展在块中系统预都分配，则无需运行时分配的块，搜索特定描述符的列表，也不再需要将指针存储到的每个数据包扩展插件。

## <a name="packet-descriptor-versionability"></a>数据包描述符 versionability

NetAdapterCx 的核心数据包描述符可以轻松地在将来的版本提供通过添加新字段到末尾，如在下图中：

![NetAdapterCx core 数据包描述符版本控制](images/packet-descriptors-3-core-descriptor-versioning.png)

了解有关 V2 字段的更高版本客户端驱动程序可以访问它们，而较旧的仅限 V1 的驱动程序将使用扩展的偏移量来跳过 V2 字段，以便他们可以访问其了解的字段。 此外，每个扩展可以是版本控制中相同的方式，如图所示：

![NetAdapterCx 数据包扩展版本控制](images/packet-descriptors-4-extension-versioning.png)

了解新的扩展插件的客户端驱动程序可以使用它。 其他客户端驱动程序可以跳过的新字段。 这将允许独立进行版本控制的数据包说明符的不同部分。

## <a name="packet-descriptors-and-datapath-performance"></a>数据包描述符和数据路径性能

所述的可扩展性功能以前提供了福利，以帮助满足性能要求的 Nic 是 capabable 的客户端驱动程序的数百个千兆位每秒，具有数千个队列：

1. 保留的数据包描述符尽可能紧凑以提高 CPU 缓存命中数，如功能和不使用扩展的占用空间描述符中的 0 字节。 
2. 没有任何指针取消引用，仅偏移量的算术因为扩展是在行，这不仅节省空间，而且还有助于使用 CPU 缓存命中数。 
3. 扩展分配在创建队列时，因此驱动程序无需分配和释放活动的数据路径中的内存或处理后备链的上下文块的列表。

## <a name="using-packet-extensions"></a>使用数据包扩展 

> [!IMPORTANT]
> 目前，客户端驱动程序仅限于[由操作系统定义的预先存在数据包扩展](#predefined-packet-extension-constants-and-helper-methods)。

### <a name="registering-packet-extensions"></a>注册包扩展

使用数据包扩展 NIC 客户端驱动程序中的第一步是声明支持的硬件卸载。 当播发对卸载 LSO 校验和等的支持时，NetAdapterCx 会自动注册代表你的相关的数据包扩展。

对的校验和及 LSO 卸载广告硬件的代码示例，请参阅[NetAdapterCx 硬件卸载功能](netadaptercx-hardware-offloads.md)。

### <a name="querying-packet-extension-offsets-for-datapath-queues"></a>查询数据包扩展的数据路径队列偏移量

通过声明您的硬件的注册数据包扩展卸载支持后，将需要访问每个处理数据包的扩展偏移量。 若要减少超出您的驱动程序的调用并提高性能，可以查询的偏移量为你的扩展期间*EvtNetAdapterCreateTx (Rx) 队列*回调函数和存储队列上下文中的偏移量信息。 

有关查询扩展偏移量，并将其存储在队列上下文中的示例，请参阅[传输和接收队列](transmit-and-receive-queues.md)。

### <a name="getting-packet-extensions-at-runtime"></a>在运行时获取包扩展

一旦您队列的上下文中存储扩展偏移量，你可以使用它们的每当您需要在扩展中的信息。 例如，您可以调用[ **NetExtensionGetPacketChecksum** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksum/nf-checksum-netextensiongetpacketchecksum)方法，尽管您编写到传输队列的硬件的描述符：

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

NetAdapterCx 提供已知的数据包扩展常量的定义。

| Constant | 定义 |
| --- | --- |
| NET_PACKET_EXTENSION_INVALID_OFFSET | 防止无效偏移量的大小。 |
| <ul><li>NET_PACKET_EXTENSION_CHECKSUM_NAME</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1_SIZE</li></ul> | 名称、 版本和校验和数据包扩展的大小。 |
| <ul><li>NET_PACKET_EXTENSION_LSO_NAME</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1_SIZE</li></ul> | 名称、 版本和大小的大型发送卸载 (LSO) 数据包扩展。 |
| <ul><li>NET_PACKET_EXTENSION_RSC_NAME</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1_SIZE</li></ul> | 名称、 版本和接收段合并 (RSC) 数据包扩展的大小。 |

此外，NetAdapterCx 提供三个帮助器方法，后者将作为包装[ **NetExtensionGetData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extension/nf-extension-netextensiongetdata)方法。 每个方法返回一个指向适当类型的结构。

| 方法 | 结构 |
| --- | --- |
| [**NetExtensionGetPacketChecksum**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksum/nf-checksum-netextensiongetpacketchecksum) | [**NET_PACKET_CHECKSUM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksumtypes/ns-checksumtypes-_net_packet_checksum) |
| [**NetExtensionGetLargeSendSegmentation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lso/nf-lso-netextensiongetpacketlargesendsegmentation) | [**NET_PACKET_LARGE_SEND_SEGMENTATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lsotypes/ns-lsotypes-_net_packet_large_send_segmentation)
| [**NetExtensionGetPacketReceiveSegmentCoalescence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsc/nf-rsc-netextensiongetpacketreceivesegmentcoalescence) | [**NET_PACKET_RECEIVE_SEGMENT_COALESCENCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsctypes/ns-rsctypes-_net_packet_receive_segment_coalescence) |
