---
title: Reset
description: Reset
ms.assetid: 5f37eca3-08b6-4bac-9d02-8a8ebd8c1904
keywords:
- 面向连接的 NDIS WDK，重置 Nic
- CoNDIS WDK 网络，重置 Nic
- 重置 NIC WDK 网络
- Nic WDK 网络，重置
- 网络接口卡 WDK 网络，重置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b764236031721dcbbff8d3e9be5d621b96bd44d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842028"
---
# <a name="reset"></a>Reset





NDIS 可以调用微型端口驱动程序或 MCM 驱动程序的[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数来重置 NIC。

**请注意**，在重置生效之前，  AF、SAP 和 VC 句柄有效，在重置后有效。

 

下图显示了向微型端口驱动程序发出重置请求的客户端。

![说明客户端向微型端口驱动程序发出重置请求的关系图](images/cm-27.png)

下图显示了向 MCM 驱动程序发出重置请求的客户端。

![说明向 mcm 驱动程序发出 reset 请求的客户端的关系图](images/fig1-26.png)

当面向连接的基础驱动程序重置 NIC 时，NDIS 会通过使用 NDIS\_状态调用协议的[**ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)函数来通知每个绑定协议\_RESET\_START。

正在重置微型端口驱动程序或 MCM 驱动程序的 NIC 时，NDIS 不会接受协议启动的发送和请求到微型端口驱动程序或 MCM 驱动程序。 当重置正在进行时，协议驱动程序不得尝试使用[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)将数据包发送到微型端口驱动程序，或使用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)从微型端口驱动程序请求信息。

*MiniportResetEx*执行重置 NIC 所需的任何设备相关操作。 *MiniportResetEx*可以同步完成，也可以通过调用[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)异步完成：

-   如果重置已同步完成，NDIS 会调用每个绑定协议的*ProtocolCoStatusEx*函数，并将 NDIS\_状态\_RESET\_END。

-   如果重置异步完成，NDIS 会调用每个绑定协议的*ProtocolCoStatusEx*函数，并将 NDIS\_状态\_RESET\_END。

 

 





