---
title: 中间驱动程序重置操作
description: 中间驱动程序重置操作
ms.assetid: 473dce77-4636-40da-ac38-cda1676eba3f
keywords:
- 中间驱动程序 WDK 网络重置操作
- NDIS 中间驱动程序 WDK、 重置操作
- 重置中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a89ee57187b31dc742597e74ede4f6218465e70
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371826"
---
# <a name="intermediate-driver-reset-operations"></a>中间驱动程序重置操作





中间的驱动程序必须准备好处理这种情况，因为重置基础 NIC 可以删除其绑定到基础驱动程序上的未完成发送。

基础驱动程序在 NDIS 调用微型端口驱动程序由于通常重置 NIC [ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)时 NDIS 超时时排队发送或请求为 NIC 绑定正常 如果重置基础 NIC，则调用 NDIS [ **ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)(或[ **ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex)) 函数的每个绑定协议和中间驱动程序的状态为 NDIS\_状态\_重置\_开始。 微型端口驱动程序完成后重置，再次调用 NDIS *ProtocolStatusEx*(或*ProtocolCoStatusEx*) 的状态为 NDIS\_状态\_重置\_结束日期。

如果绑定的中间驱动程序已处于挂起状态的任何传输网络数据重置 NIC 是 NDIS 到该 NIC，完成这些网络数据返回到相应的状态与中间驱动程序。 完成重置时，中间驱动程序必须再次重新提交这些网络数据。

当中间驱动程序收到的状态为 NDIS\_状态\_重置\_开始，它应：

-   包含准备要传输到任何网络数据， *ProtocolStatusEx*或*ProtocolCoStatusEx*接收 NDIS\_状态\_重置\_最终通知。

-   保存任何接收的网络数据已准备好指示最多的下一个更高版本驱动程序之前， *ProtocolStatusEx*(或*ProtocolCoStatusEx*) 接收 NDIS\_状态\_重置\_最终通知。

-   清理它为正在进行中操作和 NIC 状态维护任何内部状态。

之后*ProtocolStatusEx*(或*ProtocolCoStatusEx*) 接收 NDIS\_状态\_重置\_结束时，中间驱动程序可以继续发送网络数据发出请求并进行更高级别的驱动程序的迹象。

中间的驱动程序不提供[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)函数。

 

 





