---
title: 中间驱动程序重置操作
description: 中间驱动程序重置操作
ms.assetid: 473dce77-4636-40da-ac38-cda1676eba3f
keywords:
- 中间驱动程序 WDK 网络，重置操作
- NDIS 中间驱动程序 WDK，重置操作
- 重置中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7bb893e24577f879b3f2e1a62fc84cc7d6b119b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844180"
---
# <a name="intermediate-driver-reset-operations"></a>中间驱动程序重置操作





中间驱动程序必须准备好处理其对绑定到基础驱动程序的未完成发送的情况，因为基础 NIC 被重置。

基础驱动程序通常会重置 NIC，因为当 NDIS 超时发送或绑定到 NIC 的请求时，NDIS 会调用微型端口驱动程序的[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数。 如果重置基础 NIC，NDIS 会将每个绑定协议和中间驱动程序的[**ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)（或[**ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)）函数称为 NDIS\_状态\_reset\_START。 当微型端口驱动程序完成重置后，NDIS 将再次调用*ProtocolStatusEx*（或*ProtocolCoStatusEx*），状态为 NDIS\_状态\_reset\_END。

重置 NIC 时，如果绑定的中间驱动程序具有任何挂起到该 NIC 的传输网络数据，NDIS 会使用适当的状态将这些网络数据备份回中间驱动程序。 当重置完成时，中间驱动程序必须重新提交这些网络数据。

当中间驱动程序接收到 NDIS\_状态的状态时\_RESET\_START，应：

-   在*ProtocolStatusEx*或*PROTOCOLCOSTATUSEX*接收到 NDIS\_状态\_RESET\_END 通知之前，请保留可供传输的任何网络数据。

-   在*ProtocolStatusEx*（或*ProtocolCoStatusEx*）接收到 NDIS\_状态\_RESET\_END 通知之前，请将任何已接收的网络数据保存到下一个更高的驱动程序中。

-   清理它为正在进行的操作和 NIC 状态维护的任何内部状态。

*ProtocolStatusEx*（或*PROTOCOLCOSTATUSEX*）接收 NDIS\_状态\_RESET\_END 后，中间驱动程序可以继续发送网络数据、发出请求并向更高级别的驱动程序发出指示。

中间驱动程序未提供[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数。

 

 





