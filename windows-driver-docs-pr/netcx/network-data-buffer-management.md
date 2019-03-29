---
title: 网络数据缓冲区管理
description: 网络数据缓冲区管理
ms.assetid: BFE1D376-88FB-41CB-AB6D-A0D6BB83128C
keywords:
- WDF 网络适配器类扩展缓冲区管理器中，网络数据缓冲区管理
ms.date: 02/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 37a1fe52288bbb0e45666178573f861baac3be69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563970"
---
# <a name="network-data-buffer-management"></a>网络数据缓冲区管理

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

缓冲区管理是一个功能，使网络接口卡 (NIC) 客户端驱动程序和操作系统协同工作时分配系统内存的数据包数据缓冲区的传输 （德克萨斯州） 和接收 (Rx) 数据路径。 这可能导致更快的 nic 的性能、 更简单的内存生存期管理 NIC 的客户端驱动程序，并更好地控制系统内存。

## <a name="the-benefits-of-buffer-management-in-netadaptercx"></a>在 NetAdapterCx 缓冲区管理的好处

所选的位置从数据包有效负载的系统内存分配数据缓冲区的数据路径性能至关重要。 在 NetAdapterCx，缓冲区管理模型优化对于支持 DMA 的 NIC 硬件，并充分利用它的客户端驱动程序的最佳方式是让系统为 Tx 和 Rx 路径分配代表他们的数据缓冲区。 但是，客户端驱动程序可能仍会影响的位置，以便它们可以轻松地使用由客户端的硬件系统如何分配数据缓冲区。 

例如，考虑典型 DMA 支持的 NIC。 有几这种方法的好处：

1. 数据缓冲区将分配和释放由系统。 因此，客户端驱动程序，将释放的内存生存期管理的工作负担。
2. 系统可确保已分配的数据缓冲区的基于声明的客户端驱动程序功能的 NIC 硬件是 DMA 就绪。 然后，客户端驱动程序可以只需进行编程的数据缓冲区到作为其硬件-而无需执行任何其他 DMA 映射操作。
3. 系统可能需要考虑到上层应用程序的需求时分配数据缓冲区，因此它就能确定针对全局的端到端性能，而不是本地的端到端性能进行优化。

对于非 DMA capabile Nic 诸如基于 USB 的网络硬件保护装置，或对于其他/高级软件的 Nic，缓冲区管理模型还提供了一个选项以将数据缓冲区管理保留完全客户端驱动程序。 

## <a name="how-to-leverage-buffer-management"></a>如何利用缓冲区管理

> [!IMPORTANT]
> 如果您的硬件支持 DMA，需要设置 Rx 和 Tx 功能之前创建 WDFDMAENABLER 对象。 当配置与你 WDFDMAENABLER 对象[ **WDF_DMA_ENABLER_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)结构，请务必设置**WdmDmaVersionOverride**成员添加到**3**指定 DMA 版本 3。

可以选择将缓冲区管理，请执行以下步骤：

1. 开始您的网络适配器，但在通过调用[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)，告诉您的硬件的数据缓冲区功能和限制使用系统[ **NET_ADAPTER_RX_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/ns-netadapter-_net_adapter_rx_capabilities)并[ **NET_ADAPTER_TX_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/ns-netadapter-_net_adapter_tx_capabilities)数据分别结构 Rx 和 Tx 路径。 
2. 通过调用初始化函数之一初始化两个功能结构。 例如，使用 DMA 支持的 NIC 客户端驱动程序[ **NET_ADAPTER_TX_CAPABILITIES_INIT_FOR_DMA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_tx_capabilities_init_for_dma)并[ **NET_ADAPTER_RX_CAPABILITIES_INIT_SYSTEM_MANAGED** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_rx_capabilities_init_system_managed)来声明其硬件 DMA 容量和指示系统来全面管理代表其自身的数据缓冲区。
3. 传递到在初始化的 Tx 和 Rx 功能结构[ **NetAdapterSetDatapathCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)方法。


## <a name="example"></a>示例

下面的示例说明了如何开始在 NIC 客户端驱动程序中使用的缓冲区管理器在上一部分中所述的基本步骤。 该示例使用 DMA Tx 和 Rx，，因此它之前创建一个 WDFDMAENABLER 对象，它存储在其设备上下文空间。 

请注意该示例还将有关其片段缓冲区的一些提示，首先初始化 Tx 和 Rx 功能结构。 NetAdapterCx 和协议驱动程序可以使用这些提示以提高性能。

为清楚起见，错误处理已被省略。

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
