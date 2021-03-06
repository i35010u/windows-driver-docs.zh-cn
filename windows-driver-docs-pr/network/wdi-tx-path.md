---
title: WDI TX 路径
description: 本部分介绍 WDI TX 路径
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d5ea9f2d241f2a09d3889e3d0653883282f8e23
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247975"
---
# <a name="wdi-tx-path"></a>WDI TX 路径


## <a name="tx-path-components"></a>TX 路径组件


下图显示了 TX 路径组件。

![wdi tx 路径](images/wdi-tx-path-block-diagram.png)

## <a name="tx-descriptors"></a>TX 描述符


TAL 使用目标 TX 描述符 (TTD) 通知目标为帧的大小和位置。

不同的目标 WLAN 设备可能具有不同的 TTD 定义。 因此，TTD 编程是在 TAL 中根据 WDI 提供的信息来完成的。 若要对 TTD 进行编程，WDI 指定了 (NBL) 的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) ，通过该列表可以访问帧元数据（如框架 ID、扩展的 TID、适用的任务卸载和加密免除操作）。

TAL 将 TTD 和 TX 帧传输到目标。 通过 TTD 中的元数据和框架标头中的字段，目标可以确定传输帧的目标接收方以及如何传输。

最终，目标会传输该帧，并在传输 (并且可能传输) 完成时通知主机。 目标使用 TX 完成消息来指定传输是否成功，以及传输已完成的帧的 Id。

## <a name="basic-operation"></a>基本操作


传输数据帧涉及 WLAN 主机 TX 软件中的以下步骤。

1.  如果 WDI 在 PeerTID 队列模式) 下运行，WDI 将从 NDIS 获取 NBL 并执行 TX 分类 (。
2.  NBL 链接到通过查询 TAL 获取的 TTD。 为提高效率，TAL 可以从后备链表列表预分配 TTDs。
3.  TxMgr 根据 **TargetPriorityQueueing** 模式，根据 PeerTID 或端口对传输帧排队。
4.  TxMgr 向 TxEngine 提供 NBL 和附加的 TTD，然后将其传递给等到以传输到目标。 TxEngine/等到不会将帧排队 (例如，在将它们提供给 DMA) 之前。
5.  TxEngine 指示 TxEngine/target 拥有的帧的已更新 TX 状态使用传输完成 (，并在适用的) 发送完成指示。
6.  当帧都传输完成时 (并且如果需要，TX 完成) ，TxMgr 将使用该帧 ID 查找 NBL，将 TTD 返回到 TxEngine 的池，并将帧发送到 NDIS。

## <a name="host---target-tx-flow-control"></a>主机-目标 TX 流控制


TX 流控制是避免等到和目标资源的巨大必要。

### <a name="the-target-credit-scheme-and-the-pauseresume-mechanism"></a>目标-信用方案和暂停/继续机制

TxMgr 根据基于信用的方案将 TX 帧传输到目标。 目标为 TX 引擎提供了信用更新指示，以指定可用于目标上的其他帧的资源。 在 TTD 编程时确定目标上每个帧使用的信用额度。 作为给定队列中的发送操作的一部分，传递给 TxEngine 的帧数受到在按 FIFO 顺序排列的可用信用额度和行头的帧成本的限制。

对于 TxMgr，信用额度具有抽象单位。 目标/TxEngine 应使用任何信用定义对于特定实现最有用。

TAL 使用暂停/恢复指示停止/恢复来自给定端口的 TX 流量流，或发送到具有给定 TID 的特定接收方。 如果 TxEngine 获取了发送请求，而可用信用额度低于最大帧开销，则 TxEngine 将在所有端口之间暂停来自 TxMgr (的流量，) 直到目标的下一次信用更新为止。

当 WDI 处于 "端口队列" 模式 (**TargetPriorityQueueing** 等于 TRUE) 时，仅在端口或适配器级别上允许/定义暂停/继续指示，因为缺少对等互连、TID 分类和排队。

### <a name="limiting-the-maximum-frame-count-for-send-operations"></a>限制发送操作的最大帧计数

为了避免等到中的临时队列需要 (例如，DMA 速率匹配队列) ，在发送操作中 TxMgr 传递到 TxEngine 的帧数受 TxEngine 指定的最大计数限制。 此限制可能特定于 TxMgr 尝试发送的队列，并随时间而变化，因为等到中有更多可用空间。

## <a name="host---target-tx-transfer-scheduling"></a>主机-目标 TX 传输计划


TxMgr 使用单个 TX 线程将帧提交到 TxEngine。 只要存在累积队列，TX 线程就会主动地将帧提交到 TxEngine。

TxMgr 根据队列模式按以下方式计划队列。

对于 WDI 端口队列 (**TargetPriorityQueueing** 等于 TRUE) ，TxMgr 服务使用不足轮循机制 (DRR) 跨所有囤积的端口队列。

对于 WDI PeerTID 队列 (**TargetPriorityQueueing** 等于 FALSE) ，TxMgr 服务会根据 AC 优先级进行排队，而不会从而使任何队列，并确保等到和 target 中的任何瓶颈资源在 RA-TID 流中以公平的方式共享。 它可防止慢速流消耗不相称的资源份额。

通常，计划程序使用 DRR 选择要在任何给定时间传输的对等-TID 队列。 对于每个队列，DRR 会关联一个量程参数，用于限制每个循环中从队列发送的八进制数。 TxEngine 在涉及队列的每个发送操作中更新此参数，以匹配一个或两个传输机会的预期大小。

通常，DRR 计划程序仅提供与最高优先级的积压 AC 关联的 RA-TID 队列。 若要防止不足，计划程序会定期在所有囤积队列中执行 DRR。

### <a name="priority-mapping-for-ihv-reserved-extended-tids"></a>IHV 保留扩展 TIDs 的优先级映射

Ihv 保留范围内的由 IHV 注入的帧会映射到以下扩展的 ACs，目的是制定优先级计划。 该表按优先级提高。

| 扩展 TID | 扩展 AC |
| - | - |
| 17 | AC \_ BK |
| 18 | AC \_ |
| 19 | AC \_ VI |
| 20 | AC \_ VO |
| 21 | AC \_ PR0 |
| 22 | AC \_ PR1 |
| 23 | AC \_ pr2)  |
| 24 | AC \_ PR3 |

对于 WDI 端口队列，无论扩展 TID 如何，所有注入的帧都同样被视为相同。

## <a name="txmgr-txengine-interface"></a>TxMgr-TxEngine 接口


### <a name="requests-to-txengine"></a>对 TxEngine 的请求

-   [*微型端口 \_ WDI \_ TX \_ 中止*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_abort)
-   [*微型端口 \_ WDI \_ TX \_ 数据 \_ 发送*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_data_send)
-   [*\_WDI \_ TX \_ TAL \_ \_ 按 \_ 顺序排列的微型端口*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_queue_in_order)
-   [*微型端口 \_ WDI \_ TX \_ TAL \_ 发送*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send)
-   [*微型端口 \_ WDI \_ TX \_ TAL \_ 发送 \_ 完成*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send_complete)
-   [*微型端口 \_ WDI \_ TX \_ 目标 \_ DESC \_ DEINIT*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit)
-   [*微型端口 \_ WDI \_ TX \_ 目标 \_ DESC \_ INIT*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init)

### <a name="indications-from-txengine"></a>TxEngine 中的指示

-   [*NDIS \_ WDI \_ TX 取消 \_ 排队 \_ IND*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_dequeue_ind)
-   [*NDIS \_ WDI \_ TX \_ 传输 \_ 完成 \_ IND*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_transfer_complete_ind)
-   [*NDIS \_ WDI \_ TX \_ SEND \_ COMPLETE \_ IND*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_complete_ind)
-   [*NDIS \_ WDI \_ TX \_ 查询 \_ RA \_ TID \_ 状态*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_query_ra_tid_state)

### <a name="tx-specific-control-requests"></a>TX 特定控制请求

-   [*微型端口 \_ WDI \_ TX \_ 对等 \_ 积压*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_peer_backlog)

### <a name="tx-specific-control-indications"></a>TX 特定控制指示

-   [*NDIS \_ WDI \_ TX \_ SEND \_ 暂停 \_ IND*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_pause_ind)
-   [*NDIS \_ WDI \_ TX \_ SEND \_ RESTART \_ IND*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_restart_ind)
-   [*NDIS \_ WDI \_ TX \_ RELEASE \_ 帧 \_ IND*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_release_frames_ind)
-   [*NDIS \_ WDI \_ TX \_ 注入 \_ 帧 \_ IND*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_inject_frame_ind)

## <a name="related-topics"></a>相关主题


[WDI TX 路径函数](/windows-hardware/drivers/ddi/_netvista/)

[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)

[**WDI \_ TXRX \_ 功能**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_txrx_target_capabilities)

 

