---
title: WDI TX 路径
description: 本部分介绍 WDI TX 路径
ms.assetid: 8DF3E82E-761E-4A90-A789-1CB8EE8F0377
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4ed4b88e8d276c64d3cc4eba7b0831b1eaaaec7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361746"
---
# <a name="wdi-tx-path"></a>WDI TX 路径


## <a name="tx-path-components"></a>TX 路径组件


下图显示了 TX 路径组件。

![wdi tx 路径](images/wdi-tx-path-block-diagram.png)

## <a name="tx-descriptors"></a>TX 描述符


谈论使用目标 TX 描述符 (TTD) 来通知目标的大小和位置的帧。

不同的目标 WLAN 设备可能具有不同的 TTD 的定义。 因此，TTD 编程中谈论，基于由 WDI 提供的信息完成。 要编制 TTD，WDI 指定[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388) (NBL) 通过框架元数据，例如帧 ID 的 TID、 适用的任务卸载和加密进行扩展例外的操作，都可以访问。

谈论将 TTD 和 TX 帧传输到目标。 从 TTD 和帧的标头中的字段中的元数据，目标可以确定传输帧以及如何将其传输的目标接收方。

最终，目标传输将在帧和传输，则可能传输） 完成时通知宿主。 目标使用指定传输是否成功，将 TX 完成消息和已完成，但其传输的帧的 Id。

## <a name="basic-operation"></a>基本操作


传输的数据帧 WLAN 主机 TX 软件中的步骤如下。

1.  WDI 从 NDIS 获取 NBL，并执行 TX 分类 （如果 WDI PeerTID 排队模式中运行）。
2.  NBL 链接到通过查询谈论获取 TTD。 为提高效率，谈论可能预 TTDs 分配从后备链列表。
3.  TxMgr 队列基于 PeerTID 或端口，具体取决于传输帧**TargetPriorityQueueing**模式。
4.  TxMgr 提供到 TxEngine，又将其传递给传输到目标 TIL NBL 和附加的 TTD。 TxEngine / 磁贴不会排队帧 （例如之前使它们可为 DMA）。
5.  TxEngine 指示的帧归 TxEngine/目标使用传输完成更新的 TX 状态 （和传输完成指示如果适用）。
6.  帧这两个传输完成后 （并且如果需要，TX 完整）、 TxMgr 查找使用框架 ID NBL，便会回到 TTD TxEngine 的池，并发送完成到 NDIS 帧。

## <a name="host---target-tx-flow-control"></a>主机-面向 TX 流控制


TX 流控制是避免淹没 TIL 和目标资源所必需的。

### <a name="the-target-credit-scheme-and-the-pauseresume-mechanism"></a>目标信用额度方案和暂停/恢复机制

TxMgr 排队，并将 TX 帧传输到根据信用额度基于方案的目标。 目标提供了与目标系统指定可用于其他帧的资源的信用额度更新指示 TX 引擎。 在 TTD 编程时确定的信用额度用完每个目标上的帧数。 帧数传递给 TxEngine 受可用信用额度和按 FIFO 顺序行开头的帧的成本限制从给定队列的发送操作的一部分。

到 TxMgr，信用额度具有抽象单位。 目标/TxEngine 应使用的信用额度的任何定义是最适用于特定实现。

谈论使用暂停/恢复的指示来停止/恢复 TX 通信流量从给定的端口，或要发送到特定接收端使用给定的 TID。 如果 TxEngine 获取发送请求时可用的信用额度小于最大帧成本，TxEngine 将暂停目标在下一步信用额度更新之前，来自 TxMgr （跨所有端口） 的流量。

当 WDI 处于端口排队模式 (**TargetPriorityQueueing**等于 TRUE)，暂停/恢复指示是仅允许定义在由于没有对等方，TID 分类端口或适配器级别和队列。

### <a name="limiting-the-maximum-frame-count-for-send-operations"></a>限制发送操作的最大帧计数

若要避免临时队列中 （例如，DMA 速率匹配队列） TIL 的需要，将传递给 TxEngine 的 TxMgr 发送操作中的帧数受到 TxEngine 由指定的最大计数。 此限制可能是特定于队列 TxMgr 尝试从发送，并随着更多的空间现已推出 TIL 发生变化时。

## <a name="host---target-tx-transfer-scheduling"></a>主机-目标 TX 传输计划


TxMgr 使用单个 TX 线程提交 TxEngine 的帧。 没有主动提交 TxEngine 的帧，只要积压的队列 TX 线程。

TxMgr 计划队列按以下方式具体取决于排队模式。

WDI 端口队列 (**TargetPriorityQueueing**等于 true 时适用)、 跨所有囤积的端口队列使用患轮循机制 (DRR) TxMgr 服务队列。

WDI PeerTID 队列 (**TargetPriorityQueueing**等于 FALSE)，TxMgr 服务根据 AC 优先级队列的而不造成任何队列，并确保任何瓶颈 TIL 中的资源和目标所共享的远程协助 TID公平的方式的流。 它会阻止慢速流使用此类资源的过多共享。

一般情况下，计划程序使用 DRR 选择要在任何给定时间从传输的对等方 TID 队列。 对于每个队列，DRR 将限制发送队列中每一轮的八进制数的量程参数相关联。 TxEngine 更新此参数在每个发送操作中涉及队列以匹配一个或两个传输机会的预期的大小。

一般情况下，与最高优先级囤积 AC DRR 计划程序服务的远程协助 TID 队列、 关联。 若要防止资源不足，计划程序内定期执行 DRR 囤积的所有队列。

### <a name="priority-mapping-for-ihv-reserved-extended-tids"></a>优先级映射 IHV 保留扩展的 Tid

帧由与 IHV 保留的范围映射到以下扩展 TID IHV 注入扩展的优先级计划用于 ACs。 表是按顺序递增的优先级。

|              |        |        |        |        |         |         |         |         |
|--------------|--------|--------|--------|--------|---------|---------|---------|---------|
| 扩展的 TID | 17     | 18     | 19     | 20     | 21      | 22      | 23      | 24      |
| 扩展的交流  | AC\_BK | AC\_BE | AC\_VI | AC\_VO | AC\_PR0 | AC\_PR1 | AC\_PR2 | AC\_PR3 |

 

WDI 端口队列，而不考虑扩展 TID 同等对待所有注入的帧中。

## <a name="txmgr-txengine-interface"></a>TxMgr TxEngine 接口


### <a name="requests-to-txengine"></a>对 TxEngine 请求

-   [*MINIPORT\_WDI\_TX\_ABORT*](https://msdn.microsoft.com/library/windows/hardware/mt297587)
-   [*MINIPORT\_WDI\_TX\_DATA\_SEND*](https://msdn.microsoft.com/library/windows/hardware/mt297588)
-   [*微型端口\_WDI\_TX\_谈论\_队列\_IN\_顺序*](https://msdn.microsoft.com/library/windows/hardware/mt297590)
-   [*MINIPORT\_WDI\_TX\_TAL\_SEND*](https://msdn.microsoft.com/library/windows/hardware/mt297591)
-   [*MINIPORT\_WDI\_TX\_TAL\_SEND\_COMPLETE*](https://msdn.microsoft.com/library/windows/hardware/mt297592)
-   [*MINIPORT\_WDI\_TX\_TARGET\_DESC\_DEINIT*](https://msdn.microsoft.com/library/windows/hardware/mt297593)
-   [*MINIPORT\_WDI\_TX\_TARGET\_DESC\_INIT*](https://msdn.microsoft.com/library/windows/hardware/mt297594)

### <a name="indications-from-txengine"></a>指示从 TxEngine

-   [*NDIS\_WDI\_TX\_DEQUEUE\_IND*](https://msdn.microsoft.com/library/windows/hardware/mt297609)
-   [*NDIS\_WDI\_TX\_TRANSFER\_COMPLETE\_IND*](https://msdn.microsoft.com/library/windows/hardware/mt297616)
-   [*NDIS\_WDI\_TX\_SEND\_COMPLETE\_IND*](https://msdn.microsoft.com/library/windows/hardware/mt297613)
-   [*NDIS\_WDI\_TX\_查询\_RA\_TID\_状态*](https://msdn.microsoft.com/library/windows/hardware/mt297611)

### <a name="tx-specific-control-requests"></a>TX 特定控制请求

-   [*微型端口\_WDI\_TX\_对等方\_积压工作*](https://msdn.microsoft.com/library/windows/hardware/mt297589)

### <a name="tx-specific-control-indications"></a>TX 特定控件指示

-   [*NDIS\_WDI\_TX\_SEND\_PAUSE\_IND*](https://msdn.microsoft.com/library/windows/hardware/mt297614)
-   [*NDIS\_WDI\_TX\_SEND\_RESTART\_IND*](https://msdn.microsoft.com/library/windows/hardware/mt297615)
-   [*NDIS\_WDI\_TX\_RELEASE\_FRAMES\_IND*](https://msdn.microsoft.com/library/windows/hardware/mt297612)
-   [*NDIS\_WDI\_TX\_INJECT\_FRAME\_IND*](https://msdn.microsoft.com/library/windows/hardware/mt297610)

## <a name="related-topics"></a>相关主题


[WDI TX 路径函数](https://msdn.microsoft.com/library/windows/hardware/mt269153)

[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[**WDI\_TXRX\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/dn898187)

 

 






