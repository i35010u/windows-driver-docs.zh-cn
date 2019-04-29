---
title: WDI RX 路径
description: 本部分介绍 WDI RX 路径
ms.assetid: EEEA7181-4A24-4F40-8A44-65EC38D1A867
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac3b28a72688b4738421722453b9635c7f7f4d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356825"
---
# <a name="wdi-rx-path"></a>WDI RX 路径


## <a name="rx-path-components"></a>RX 路径组件


下图显示了 RX 路径组件。

![wdi 接收路径](images/wdi-receive-path-block-diagram.png)

## <a name="rx-manager-rxmgr"></a>RX 管理器 (RxMgr)


RX 管理器执行接收未卸载到目标或 RxEngine 由执行的处理步骤。

| RX 函数            | 描述                                                                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MSDU 放弃           | 放弃 MSDUs 但出现错误。                                                                                                                                                                      |
| 队列和限制 | 管理 DPC 监视器以防止从调度级别过多指示 DPC，按和太长错误检查。 向 RxEngine 帮助进行限制，请提供反压。 |

 

## <a name="rxengine"></a>RxEngine


RxEngine 发送和接收来自目标的数据同步消息，解释 RX 描述符格式，并管理直接硬件到软件 RX Dma 的缓冲区。

| RX 函数                             | 描述                                                                                                                                                                                                                                              |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 构造主机到目标消息     | 构造主机到目标数据与路径相关的消息。                                                                                                                                                                                                     |
| 目标主机消息解析          | 分析和处理目标主机的数据同步消息，如[ *NdisWdiRxInorderDataIndication*](https://msdn.microsoft.com/library/windows/hardware/mt297606)。                                                                                                          |
| 目标 RX 描述符的解释 | 用于查询特定于目标的说明符中 RX 帧特性提供的接口 （函数）。                                                                                                                                                   |
| RX FIFO 管理                      | 提供可访问目标的先进先出用于发布的目标来填充的空 RX 缓冲区。 从 FIFO 期间删除缓冲区[ *NdisWdiRxInorderDataIndication* ](https://msdn.microsoft.com/library/windows/hardware/mt297606)处理，并提供替换空缓冲区。 |
| RX 缓冲池管理               | 维护的 DMA 传输的接收帧缓冲区的池。                                                                                                                                                                                           |
| MPDU 放弃                            | 放弃 MPDUs 但出现错误。 目标指示接收帧标记丢弃-例如，由于 FCS 错误或 ARQ 重复错误。 如果它未实现的目标，这会仅完成。                                              |
| MPDU 重新排序                            | 在 RX 重新排序数组中的顺序存储 MPDUs，直到缺少前面 MPDUs 到达。 如果它未实现的目标，这会仅完成。                                                                                                   |
| MPDU PN chk                             | 如果不会卸载到目标，这只会完成。                                                                                                                                                                                                  |
| MSDU 碎片重组                | 如果不会卸载到目标，这只会完成。                                                                                                                                                                                                  |

 

## <a name="rx-path-requests-and-indications"></a>RX 路径请求和指示


RX 路径请求和指示函数的参考，请参阅[WDI RX 路径函数](https://msdn.microsoft.com/library/windows/hardware/mt269105)。

## <a name="related-topics"></a>相关主题


[*NdisWdiRxInorderDataIndication*](https://msdn.microsoft.com/library/windows/hardware/mt297606)

[WDI RX 路径函数](https://msdn.microsoft.com/library/windows/hardware/mt269105)

 

 






