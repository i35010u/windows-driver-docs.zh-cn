---
title: WDI TX 路径
description: 本部分介绍 WDI TX 路径
ms.assetid: 8DF3E82E-761E-4A90-A789-1CB8EE8F0377
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51af368e4aabd1b6f01cd18a64f2a4579b2d96e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841713"
---
# <a name="wdi-tx-path"></a>WDI TX 路径


## <a name="tx-path-components"></a>TX 路径组件


下图显示了 TX 路径组件。

![wdi tx 路径](images/wdi-tx-path-block-diagram.png)

## <a name="tx-descriptors"></a>TX 描述符


TAL 使用目标 TX 描述符（TTD）来向目标通知帧的大小和位置。

不同的目标 WLAN 设备可能具有不同的 TTD 定义。 因此，TTD 编程是在 TAL 中根据 WDI 提供的信息来完成的。 若要对 TTD 进行编程，WDI 指定了[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)（NBL），通过该缓冲区可访问帧元数据（如框架 ID、扩展的 TID、适用的任务卸载和加密免除操作）。

TAL 将 TTD 和 TX 帧传输到目标。 通过 TTD 中的元数据和框架标头中的字段，目标可以确定传输帧的目标接收方以及如何传输。

最终，目标会传输该帧，并在传输（可能传输）完成时通知主机。 目标使用 TX 完成消息来指定传输是否成功，以及传输已完成的帧的 Id。

## <a name="basic-operation"></a>基本操作


传输数据帧涉及 WLAN 主机 TX 软件中的以下步骤。

1.  WDI 从 NDIS 获取 NBL 并执行 TX 分类（如果 WDI 在 PeerTID 排队模式下操作）。
2.  NBL 链接到通过查询 TAL 获取的 TTD。 为提高效率，TAL 可以从后备链表列表预分配 TTDs。
3.  TxMgr 根据**TargetPriorityQueueing**模式，根据 PeerTID 或端口对传输帧排队。
4.  TxMgr 向 TxEngine 提供 NBL 和附加的 TTD，然后将其传递给等到以传输到目标。 TxEngine/等到不会对帧进行排队（例如，在将它们提供给 DMA 之前）。
5.  TxEngine 指示 TxEngine/目标拥有的帧的已更新 TX 状态使用传输完成（如果适用，则发送完成指示）。
6.  当帧既完成传输（并在需要时，TX 完成）时，TxMgr 将使用该帧 ID 查找 NBL，将 TTD 返回到 TxEngine 的池，并将帧发送到 NDIS。

## <a name="host---target-tx-flow-control"></a>主机-目标 TX 流控制


TX 流控制是避免等到和目标资源的巨大必要。

### <a name="the-target-credit-scheme-and-the-pauseresume-mechanism"></a>目标-信用方案和暂停/继续机制

TxMgr 根据基于信用的方案将 TX 帧传输到目标。 目标为 TX 引擎提供了信用更新指示，以指定可用于目标上的其他帧的资源。 在 TTD 编程时确定目标上每个帧使用的信用额度。 作为给定队列中的发送操作的一部分，传递给 TxEngine 的帧数受到在按 FIFO 顺序排列的可用信用额度和行头的帧成本的限制。

对于 TxMgr，信用额度具有抽象单位。 目标/TxEngine 应使用任何信用定义对于特定实现最有用。

TAL 使用暂停/恢复指示停止/恢复来自给定端口的 TX 流量流，或发送到具有给定 TID 的特定接收方。 如果 TxEngine 在可用信用额度低于最大帧成本时获得发送请求，则 TxEngine 将从 TxMgr （跨所有端口）暂停流量，直到目标的下一个信用更新。

当 WDI 处于 "端口队列" 模式（**TargetPriorityQueueing**等于 TRUE）时，仅在端口或适配器级别上允许/定义暂停/继续指示，因为缺少对等互连、TID 分类和排队。

### <a name="limiting-the-maximum-frame-count-for-send-operations"></a>限制发送操作的最大帧计数

为了避免在等到中使用临时队列（例如，DMA 速率匹配队列），TxMgr 在发送操作中传递到 TxEngine 的帧数受 TxEngine 指定的最大计数的限制。 此限制可能特定于 TxMgr 尝试发送的队列，并随时间而变化，因为等到中有更多可用空间。

## <a name="host---target-tx-transfer-scheduling"></a>主机-目标 TX 传输计划


TxMgr 使用单个 TX 线程将帧提交到 TxEngine。 只要存在累积队列，TX 线程就会主动地将帧提交到 TxEngine。

TxMgr 根据队列模式按以下方式计划队列。

对于 WDI 端口队列（**TargetPriorityQueueing**等于 TRUE），TxMgr 服务使用不足轮循机制（DRR）跨所有囤积的端口队列进行排队。

对于 WDI PeerTID 队列（**TargetPriorityQueueing** = FALSE），TxMgr services 会根据 AC 优先级进行排队，而不会在任何队列中排队，并确保从而使和目标中的所有瓶颈资源在 RA-TID 流之间以公平的方式共享. 它可防止慢速流消耗不相称的资源份额。

通常，计划程序使用 DRR 选择要在任何给定时间传输的对等-TID 队列。 对于每个队列，DRR 会关联一个量程参数，用于限制每个循环中从队列发送的八进制数。 TxEngine 在涉及队列的每个发送操作中更新此参数，以匹配一个或两个传输机会的预期大小。

通常，DRR 计划程序仅提供与最高优先级的积压 AC 关联的 RA-TID 队列。 若要防止不足，计划程序会定期在所有囤积队列中执行 DRR。

### <a name="priority-mapping-for-ihv-reserved-extended-tids"></a>IHV 保留扩展 TIDs 的优先级映射

Ihv 保留范围内的由 IHV 注入的帧会映射到以下扩展的 ACs，目的是制定优先级计划。 该表按优先级提高。

|              |        |        |        |        |         |         |         |         |
|--------------|--------|--------|--------|--------|---------|---------|---------|---------|
| 扩展 TID | 17     | 18     | 19     | 20     | 21      | 22      | 23      | 24      |
| 扩展 AC  | AC\_BK | AC\_ | AC\_VI | AC\_VO | AC\_PR0 | AC\_PR1 | AC\_PR2) | AC\_PR3 |

 

对于 WDI 端口队列，无论扩展 TID 如何，所有注入的帧都同样被视为相同。

## <a name="txmgr-txengine-interface"></a>TxMgr-TxEngine 接口


### <a name="requests-to-txengine"></a>对 TxEngine 的请求

-   [*小型端口\_WDI\_TX\_中止*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_abort)
-   [*小型端口\_WDI\_TX\_数据\_发送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_data_send)
-   [*小型端口\_WDI\_TX\_TAL\_队列\_\_顺序*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_queue_in_order)
-   [*小型端口\_WDI\_TX\_TAL\_发送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send)
-   [*小型端口\_WDI\_TX\_TAL\_发送\_完成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send_complete)
-   [*小型端口\_WDI\_TX\_目标\_DESC\_DEINIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit)
-   [*小型端口\_WDI\_TX\_目标\_DESC\_INIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init)

### <a name="indications-from-txengine"></a>TxEngine 中的指示

-   [*NDIS\_WDI\_TX\_取消排队\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_dequeue_ind)
-   [*NDIS\_WDI\_TX\_传输\_完成\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_transfer_complete_ind)
-   [*NDIS\_WDI\_TX\_发送\_完成\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_complete_ind)
-   [*NDIS\_WDI\_TX\_查询\_RA\_TID\_状态*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_query_ra_tid_state)

### <a name="tx-specific-control-requests"></a>TX 特定控制请求

-   [*小型端口\_WDI\_TX\_对等\_积压*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_peer_backlog)

### <a name="tx-specific-control-indications"></a>TX 特定控制指示

-   [*NDIS\_WDI\_TX\_发送\_暂停\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_pause_ind)
-   [*NDIS\_WDI\_TX\_发送\_重启\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_restart_ind)
-   [*NDIS\_WDI\_TX\_RELEASE\_帧\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_release_frames_ind)
-   [*NDIS\_WDI\_TX\_插入\_帧\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_inject_frame_ind)

## <a name="related-topics"></a>相关主题


[WDI TX 路径函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[**WDI\_TXRX\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_txrx_target_capabilities)

 

 






