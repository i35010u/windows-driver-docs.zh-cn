---
title: WDI RX 路径
description: 本部分介绍 WDI RX 路径
ms.assetid: EEEA7181-4A24-4F40-8A44-65EC38D1A867
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23dd4df927de8e5e2d4007f107c53749830bde53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842893"
---
# <a name="wdi-rx-path"></a>WDI RX 路径


## <a name="rx-path-components"></a>RX 路径组件


下图显示了 RX 路径组件。

![wdi 接收路径](images/wdi-receive-path-block-diagram.png)

## <a name="rx-manager-rxmgr"></a>RX 管理器（RxMgr）


RX 管理器执行不会卸载到目标或由 RxEngine 执行的接收处理步骤。

| RX 函数            | 描述                                                                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MSDU 放弃           | 丢弃具有错误的 MSDUs。                                                                                                                                                                      |
| 排队和限制 | 管理 DPC 监视程序以防止每个 DPC 的错误检测次数过多，调度级别过长。 适当时，提供 RxEngine 的反压，以帮助进行限制。 |

 

## <a name="rxengine"></a>RxEngine


RxEngine 在目标中发送和接收数据同步消息，解释 RX 描述符格式，并管理直接硬件到 software RX DMAs 的缓冲区。

| RX 函数                             | 描述                                                                                                                                                                                                                                              |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 主机到目标消息构造     | 构造与目标数据路径相关的消息。                                                                                                                                                                                                     |
| 目标到主机消息分析          | 分析并处理目标到主机的数据同步消息，如[*NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)。                                                                                                          |
| 目标 RX 描述符的解释 | 提供用于从特定于目标的描述符查询 RX 帧属性的接口（函数）。                                                                                                                                                   |
| RX FIFO 管理                      | 提供目标可访问的 FIFO，用于发布要填充的目标的空 RX 缓冲区。 在[*NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)处理期间删除 FIFO 中的缓冲区，并提供替换空缓冲区。 |
| RX 缓冲池管理               | 维护用于接收帧的 DMA 传输的缓冲区池。                                                                                                                                                                                           |
| MPDU 放弃                            | 丢弃具有错误的 MPDUs。 目标表示标记为丢弃的接收帧-例如，由于 FCS 错误或 ARQ 重复错误。 仅当目标未实现时，才执行此操作。                                              |
| 重新排序 MPDU                            | 在 RX 重新排序数组中按顺序存储 MPDUs，直到前面缺少 MPDUs。 仅当目标未实现时，才执行此操作。                                                                                                   |
| MPDU PN .chk                             | 仅当未将其卸载到目标时才执行此操作。                                                                                                                                                                                                  |
| MSDU 片段重组                | 仅当未将其卸载到目标时才执行此操作。                                                                                                                                                                                                  |

 

## <a name="rx-path-requests-and-indications"></a>RX 路径请求和指示


有关 RX 路径请求和指示函数引用，请参阅[WDI RX 路径函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

## <a name="related-topics"></a>相关主题


[*NdisWdiRxInorderDataIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_rx_inorder_data_ind)

[WDI RX 路径函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






