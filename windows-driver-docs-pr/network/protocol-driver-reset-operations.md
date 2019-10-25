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
ms.openlocfilehash: b15478f92db5763ec55ce910bc49fd16631ad5a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844910"
---
# <a name="protocol-driver-reset-operations"></a>协议驱动程序重置操作





协议驱动程序无法在 NDIS 6.0 和更高版本中启动重置操作。

通常，基础微型端口驱动程序会重置 NIC，因为在发送或请求操作期间 NIC 将超时。 这种情况会导致 NDIS 调用微型端口驱动程序的[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang) ，然后调用[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数。 或者，微型端口驱动程序确定 NIC 的接收功能是失效性。

如果重置由 NDIS 启动，而*MiniportResetEx*返回 NDIS\_状态\_挂起，ndis 将调用每个绑定协议驱动程序的[**ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)（或[**ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)）函数，状态为 NDIS\_\_开始\_重置状态。 当微型端口驱动程序调用[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)时，ndis 将再次调用*ProtocolStatusEx*（或*PROTOCOLCOSTATUSEX*），状态为 NDIS\_状态\_RESET\_END。

由于重置了 NIC，因此协议驱动程序必须处理可能会取消对基础 NIC 的绑定上的未完成发送的可能。 如果绑定的协议驱动程序有任何挂起的传输请求，NDIS 将指示使用适当的状态将其发送到协议驱动程序。 如果重置操作完成，则协议驱动程序必须重新提交发送请求，假设 NIC 再次操作。

如果协议驱动程序接收到 NDIS\_状态的状态\_RESET\_START，则应执行以下操作：

-   保存准备好传输的任何网络数据，直到*协议（Co）状态*接收到 NDIS\_状态\_RESET\_END 通知。

-   不要执行定向到基础微型端口驱动程序的任何 NDIS 调用，只需调用即可返回资源，例如，通过[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)返回网络数据。

*ProtocolStatusEx*（或*ProtocolCoStatusEx*）接收到 NDIS\_状态\_RESET\_结束消息后，协议驱动程序可以继续发送网络数据和 OID 请求。

 

 





