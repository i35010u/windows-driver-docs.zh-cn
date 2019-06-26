---
title: 初始化微型端口适配器
description: 初始化微型端口适配器
ms.assetid: 6d7a23dc-cc09-46d3-89d3-34e8e8f17a51
keywords:
- 微型端口适配器 WDK 连接网络、 初始化
- 适配器 WDK 连接网络、 初始化
- 初始化微型端口适配器
- 正在初始化状态 WDK 网络
- MiniportInitializeEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3433a48f2db627b6fe8fa5ce0392edb4679927ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383692"
---
# <a name="initializing-a-miniport-adapter"></a>初始化微型端口适配器





网络设备可用时，系统将加载所需的 NDIS 微型端口驱动程序，如果尚未加载。 随后，插 (PnP) 管理器发送 NDIS 插 IRP，若要启动设备。 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数以初始化网络 I/O 操作的适配器。 可以调用 NDIS *MiniportInitializeEx*在驱动程序进行初始化之后任何时间。 微型端口驱动程序初始化的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

直到[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)返回，NDIS 提交适配器正在初始化的任何请求。 适配器处于正在初始化状态。

微型端口驱动程序通常执行以下任务中的[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize):

1.  获取适配器的配置信息。

2.  获取有关适配器的硬件资源的信息。

3.  调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes) ，并提供与适配器相关联的以下属性：
    -   指向驱动程序分配的上下文区域的指针。
    -   相应的属性的标志。
    -   调用的超时间隔及其[ *MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)函数。
    -   接口类型。

4.  初始化特定于适配器的资源。

微型端口驱动程序指定的适配器属性中[ **NDIS\_微型端口\_适配器\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_attributes)结构的[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)将传递给[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)。

通常情况下， [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)分配特定于适配器的资源，按以下顺序：

1.  非分页缓冲的池的内存。

2.  [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)并[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)池 (请参阅[微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md))。

3.  旋转锁。

4.  计时器。

5.  IO 端口。

6.  DMA (请参阅[散播-聚集 DMA](scatter-gather-dma2.md))。

7.  共享的内存。

8.  中断 (请参阅[管理中断](managing-interrupts.md))。

之后[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)成功，返回该适配器处于已暂停状态。 可以调用 NDIS [ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)函数转换到正在运行状态的适配器。 有关详细信息，请参阅[启动微型端口适配器](starting-an-adapter.md)。

如果[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)返回 NDIS\_状态\_成功后，驱动程序应释放中适配器的所有资源[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数。 有关详细信息，请参阅[停止微型端口适配器](halting-a-miniport-adapter.md)。

如果[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)失败， *MiniportInitializeEx*必须释放它分配之前它将返回和适配器返回到暂停状态的所有资源.

## <a name="related-topics"></a>相关主题


[正在停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序发送和接收操作](miniport-driver-send-and-receive-operations.md)

[散播-聚集 DMA](scatter-gather-dma2.md)

[启动微型端口适配器](starting-an-adapter.md)

 

 






