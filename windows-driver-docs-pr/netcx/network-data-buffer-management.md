---
title: 网络数据缓冲区管理
description: 网络数据缓冲区管理
ms.assetid: BFE1D376-88FB-41CB-AB6D-A0D6BB83128C
keywords:
- WDF 网络适配器类扩展缓冲区管理器，网络数据缓冲区管理
ms.date: 02/20/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 89fdc71382c4dd62f0a003d4e925f9db574c97d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835510"
---
# <a name="network-data-buffer-management"></a>网络数据缓冲区管理

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

缓冲区管理是一项功能，可使网络接口卡（NIC）客户端驱动程序和操作系统在为传输（Tx）和接收（Rx）数据路径从系统内存中分配数据包数据缓冲区时一起工作。 这可能会使 NIC 更快地提高性能，并使 NIC 的客户端驱动程序的内存生存期管理更简单，并使系统更好地控制内存。

## <a name="the-benefits-of-buffer-management-in-netadaptercx"></a>NetAdapterCx 中的缓冲区管理的优点

为数据包有效负载从系统内存中分配数据缓冲区的选择是对数据路径性能至关重要的。 在 NetAdapterCx 中，缓冲管理模型针对支持 DMA 的 NIC 硬件进行了优化，并且客户端驱动程序利用它的最佳方式是让系统代表 Tx 和 Rx 路径为其分配数据缓冲区。 但是，客户端驱动程序仍会影响系统分配数据缓冲区的位置和方式，以便客户端的硬件可以轻松地使用它们。 

例如，考虑典型的支持 DMA 的 NIC。 此方法有几的好处：

1. 数据缓冲区由系统分配和释放。 因此，客户端驱动程序将从内存生存期管理的负担中释放出来。
2. 系统会根据客户端驱动程序声明的功能，确保分配的数据缓冲区为 NIC 硬件准备好 DMA。 然后，客户端驱动程序可以直接将数据缓冲区直接编程到其硬件中，而无需执行任何其他 DMA 映射操作。
3. 当分配数据缓冲区时，系统可能会考虑上层应用程序的需求，因此它可以决定优化全局端到端性能，而不是只优化本地端到端性能。

对于非 DMA capabile Nic （如基于 USB 的网络转换器）或其他高级/软件 Nic，缓冲区管理模型还提供了一个选项，用于将数据缓冲区管理完全留给客户端驱动程序使用。 

## <a name="how-to-leverage-buffer-management"></a>如何利用缓冲区管理

> [!IMPORTANT]
> 如果你的硬件具有 DMA 功能，则在设置 Rx 和 Tx 功能之前，你将需要创建一个 WDFDMAENABLER 对象。 当你用[**WDF_DMA_ENABLER_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)结构配置 WDFDMAENABLER 对象时，请确保将**WdmDmaVersionOverride**成员设置为**3**以指定 DMA 版本3。

若要选择缓冲管理，请执行以下步骤：

1. 在启动网络适配器时，但在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前，请使用[**NET_ADAPTER_RX_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/ns-netadapter-_net_adapter_rx_capabilities)和[**NET_ADAPTER_TX_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/ns-netadapter-_net_adapter_tx_capabilities)数据告知系统有关硬件的数据缓冲区的功能和约束Rx 和 Tx 路径的结构。 
2. 通过调用某个初始化函数来初始化两个功能结构。 例如，支持 DMA 的 NIC 客户端驱动程序将使用[**NET_ADAPTER_TX_CAPABILITIES_INIT_FOR_DMA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_tx_capabilities_init_for_dma)和[**NET_ADAPTER_RX_CAPABILITIES_INIT_SYSTEM_MANAGED_DMA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_rx_capabilities_init_system_managed_dma)声明其硬件 DMA capablities，并指示系统完全代表其管理数据缓冲区。
3. 将初始化的 Tx 和 Rx 功能结构传递到[**NetAdapterSetDatapathCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)方法。


## <a name="example"></a>示例

下面的示例说明了上一节中介绍的基本步骤，了解如何开始在 NIC 客户端驱动程序中使用缓冲区管理器。 该示例将 DMA 用于 Tx 和 Rx，因此它以前创建了一个在其设备上下文空间中存储的 WDFDMAENABLER 对象。 

请注意，该示例还在初始化 Tx 和 Rx 功能结构后，设置了有关其片段缓冲区的一些提示。 NetAdapterCx 和协议驱动程序可以使用这些提示来提高性能。

为清楚起见，已省略错误处理。

```C++
VOID
MyAdapterSetDatapathCapabilities(
    _In_ NETADAPTER Adapter
)
{
    // Get the device context
    PMY_DEVICE_CONTEXT deviceContext = GetMyContextFromDevice(Adapter);

    // Set various capabilities such as link layer MTU size, link layer capabilities, and power capabilities
    ...   

    // Initialize the Tx DMA capabilities structure
    NET_ADAPTER_DMA_CAPABILITIES txDmaCapabilities;
    NET_ADAPTER_DMA_CAPABILITIES_INIT(&txDmaCapabilities,
                                      deviceContext->dmaEnabler);

    // Set Tx capabilities
    NET_ADAPTER_TX_CAPABILITIES txCapabilities;
    NET_ADAPTER_TX_CAPABILITIES_INIT_FOR_DMA(&txCapabilities,
                                             &txDmaCapabilities,
                                             MAX_PACKET_SIZE,
                                             1);
    txCapabilities.FragmentRingNumberOfElementsHint = deviceContext->NumTransmitControlBlocks * MAX_PHYS_BUF_COUNT;
    txCapabilities.MaximumNumberOfFragments = MAX_PHYS_BUF_COUNT;

    // Initialize the Rx DMA capabilities structure
    NET_ADAPTER_DMA_CAPABILITIES rxDmaCapabilities;
    NET_ADAPTER_DMA_CAPABILITIES_INIT(&rxDmaCapabilities,
                                      deviceContext->dmaEnabler);

    // Set Rx capabilities
    NET_ADAPTER_RX_CAPABILITIES rxCapabilities;
    NET_ADAPTER_RX_CAPABILITIES_INIT_SYSTEM_MANAGED_DMA(&rxCapabilities,
                                                        &rxDmaCapabilities,
                                                        MAX_PACKET_SIZE + FRAME_CRC_SIZE + RSVD_BUF_SIZE,
                                                        1);
    rxCapabilities.FragmentBufferAlignment = 64;
    rxCapabilities.FragmentRingNumberOfElementsHint = deviceContext->NumReceiveBuffers;

    // Set the adapter's datapath capabilities
    NetAdapterSetDatapathCapabilities(Adapter, 
                                      &txCapabilities, 
                                      &rxCapabilities);
}
```
