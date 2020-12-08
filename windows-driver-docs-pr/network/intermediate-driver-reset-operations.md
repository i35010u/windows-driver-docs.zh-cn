---
title: 中间驱动程序重置操作
description: 中间驱动程序重置操作
keywords:
- 中间驱动程序 WDK 网络，重置操作
- NDIS 中间驱动程序 WDK，重置操作
- 重置中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d939965ba31d8df35b2ddcab753d2de858ade541
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808621"
---
# <a name="intermediate-driver-reset-operations"></a>中间驱动程序重置操作





中间驱动程序必须准备好处理其对绑定到基础驱动程序的未完成发送的情况，因为基础 NIC 被重置。

基础驱动程序通常会重置 NIC，因为当 NDIS 超时发送或绑定到 NIC 的请求时，NDIS 会调用微型端口驱动程序的 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数。 如果重置了基础 NIC，NDIS 将调用每个绑定协议的 [**ProtocolStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex) (或 [**ProtocolCoStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)) 函数，并将状态设置为 NDIS \_ 状态 \_ 重置为 " \_ 启动"。 当微型端口驱动程序完成重置后，NDIS 将再次调用 *ProtocolStatusEx* (或 *ProtocolCoStatusEx*) ，状态为 NDIS \_ 状态 \_ 重置 \_ 结束。

重置 NIC 时，如果绑定的中间驱动程序具有任何挂起到该 NIC 的传输网络数据，NDIS 会使用适当的状态将这些网络数据备份回中间驱动程序。 当重置完成时，中间驱动程序必须重新提交这些网络数据。

当中间驱动程序收到 NDIS \_ 状态 \_ 重置启动状态时 \_ ，它应：

-   在 *ProtocolStatusEx* 或 *ProtocolCoStatusEx* 收到 NDIS \_ 状态 \_ 重置结束通知之前，请保留可供传输的任何网络数据 \_ 。

-   在 *ProtocolStatusEx* (或 *PROTOCOLCOSTATUSEX*) 收到 NDIS \_ 状态 \_ 重置结束通知之前，请将任何已接收的网络数据保存到下一个更高的驱动程序中 \_ 。

-   清理它为正在进行的操作和 NIC 状态维护的任何内部状态。

在 *ProtocolStatusEx* (或 *PROTOCOLCOSTATUSEX*) 收到 NDIS \_ 状态 \_ 重置 \_ 结束后，中间驱动程序可以继续发送网络数据、发出请求并向更高级别的驱动程序发出指示。

中间驱动程序未提供 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数。

 

