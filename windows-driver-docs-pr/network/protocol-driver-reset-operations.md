---
title: 协议驱动程序重置操作
description: 协议驱动程序重置操作
ms.assetid: 862029e5-8c46-4889-80f5-15c463f228a3
keywords:
- 协议驱动程序 WDK 网络，重置操作
- NDIS 协议驱动程序 WDK，重置操作
- 重置操作 WDK NDIS 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1831e8b8c15033e75b092b686b2a5664d6f230a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385450"
---
# <a name="protocol-driver-reset-operations"></a>协议驱动程序重置操作





协议驱动程序无法启动 NDIS 6.0 及更高版本中的重置操作。

通常情况下，基础的微型端口驱动程序将重置 NIC 因为在发送或请求操作期间超时 NIC。 这种情况会导致调用微型端口驱动程序的 NDIS [ *MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang) ，并随后[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)函数。 或者，微型端口驱动程序确定 NIC 的接收功能是失效性。

如果重置启动 NDIS 和*MiniportResetEx*返回 NDIS\_状态\_挂起、 NDIS 调用[ **ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)（或[**ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex)) 函数的每个绑定的协议驱动程序的状态为 NDIS\_状态\_重置\_开始。 当微型端口驱动程序调用[ **NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismresetcomplete)，再次调用 NDIS *ProtocolStatusEx*(或*ProtocolCoStatusEx*) 与状态的 NDIS\_状态\_重置\_结束。

协议驱动程序必须处理的未完成将工作表上绑定到基础 NIC 可以取消，因为重置 NIC 的可能性。 如果绑定的协议驱动程序具有挂起的任何传输请求，NDIS 将指示发送完成到协议驱动程序，但相应的状态。 重置操作完成后，假定 NIC 将再次变为正常运行，协议驱动程序必须重新提交发送请求。

当协议驱动程序收到的状态为 NDIS\_状态\_重置\_开始，它应：

-   保存已准备好要传输到任何网络数据，*协议 (Co) 状态*接收 NDIS\_状态\_重置\_最终通知。

-   不调用任何 NDIS 定向到基础的微型端口驱动程序，调用返回资源，例如返回网络数据使用除[ **NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)。

之后*ProtocolStatusEx*(或*ProtocolCoStatusEx*) 接收 NDIS\_状态\_重置\_结束消息，协议驱动程序可以继续发送网络数据和 OID 请求。

 

 





