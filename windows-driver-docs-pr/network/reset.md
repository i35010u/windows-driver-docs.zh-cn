---
title: 重置
description: 重置
ms.assetid: 5f37eca3-08b6-4bac-9d02-8a8ebd8c1904
keywords:
- 面向连接的 NDIS WDK，重置 Nic
- CoNDIS WDK 网络，重置 Nic
- 重置 NIC WDK 网络
- Nic WDK 网络，重置
- 网络接口卡 WDK 网络，重置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59c2bd30c53299db5695d48615aeab17be59e5e4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215074"
---
# <a name="reset"></a>重置





NDIS 可以调用微型端口驱动程序或 MCM 驱动程序的 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数来重置 NIC。

**注意**   重新设置之前处于活动状态且有效且有效且在重置后有效的 AF、SAP 和 VC 句柄。

 

下图显示了向微型端口驱动程序发出重置请求的客户端。

![说明客户端向微型端口驱动程序发出重置请求的关系图](images/cm-27.png)

下图显示了向 MCM 驱动程序发出重置请求的客户端。

![说明向 mcm 驱动程序发出 reset 请求的客户端的关系图](images/fig1-26.png)

当面向连接的基础驱动程序重置 NIC 时，NDIS 会通过使用 NDIS [**ProtocolCoStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex) \_ 状态 \_ 重置启动调用协议的 ProtocolCoStatusEx 函数来通知每个绑定协议 \_ 。

正在重置微型端口驱动程序或 MCM 驱动程序的 NIC 时，NDIS 不会接受协议启动的发送和请求到微型端口驱动程序或 MCM 驱动程序。 当重置正在进行时，协议驱动程序不得尝试使用 [**NdisCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists) 将数据包发送到微型端口驱动程序，或使用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)从微型端口驱动程序请求信息。

*MiniportResetEx* 执行重置 NIC 所需的任何设备相关操作。 *MiniportResetEx* 可以同步完成，也可以通过调用 [**NdisMResetComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)异步完成：

-   如果重置同步完成，NDIS 会调用每个绑定协议的 *ProtocolCoStatusEx* 函数，并将 ndis \_ 状态 \_ 重置 \_ 结束。

-   如果重置异步完成，NDIS 将调用每个绑定协议的 *ProtocolCoStatusEx* 函数，并将 ndis \_ 状态 \_ 重置 \_ 结束。

 

