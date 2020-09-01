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
ms.openlocfilehash: d413198d64b1b141a31470d3b24f514cf27c7c8e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215166"
---
# <a name="protocol-driver-reset-operations"></a>协议驱动程序重置操作





协议驱动程序无法在 NDIS 6.0 和更高版本中启动重置操作。

通常，基础微型端口驱动程序会重置 NIC，因为在发送或请求操作期间 NIC 将超时。 这种情况会导致 NDIS 调用微型端口驱动程序的 [*MiniportCheckForHangEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang) ，然后调用 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数。 或者，微型端口驱动程序确定 NIC 的接收功能是失效性。

如果重置由 NDIS 启动并且 *MiniportResetEx* 返回 ndis \_ 状态 " \_ 挂起"，ndis 将调用每个绑定协议驱动程序的 [**ProtocolStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex) (或 [**PROTOCOLCOSTATUSEX**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)) 函数，状态为 "NDIS \_ 状态 \_ 重置" "启动" \_ 。 当微型端口驱动程序调用 [**NdisMResetComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)时，ndis 将再次调用 *ProtocolStatusEx* (或 *PROTOCOLCOSTATUSEX*) ，状态为 NDIS \_ 状态 \_ 重置 \_ 结束。

由于重置了 NIC，因此协议驱动程序必须处理可能会取消对基础 NIC 的绑定上的未完成发送的可能。 如果绑定的协议驱动程序有任何挂起的传输请求，NDIS 将指示使用适当的状态将其发送到协议驱动程序。 如果重置操作完成，则协议驱动程序必须重新提交发送请求，假设 NIC 再次操作。

当协议驱动程序收到 NDIS \_ 状态 \_ 重置启动状态时 \_ ，它应：

-   在 *协议 (Co) 状态* 收到 NDIS \_ 状态 \_ 重置结束通知之前，请保存准备好传输的任何网络数据 \_ 。

-   不要执行定向到基础微型端口驱动程序的任何 NDIS 调用，只需调用即可返回资源，例如，通过 [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)返回网络数据。

*ProtocolStatusEx* (或*PROTOCOLCOSTATUSEX*) 收到 NDIS \_ 状态 \_ 重置 \_ 结束消息后，协议驱动程序可以继续发送网络数据和 OID 请求。

 

