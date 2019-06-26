---
title: Reset
description: Reset
ms.assetid: 5f37eca3-08b6-4bac-9d02-8a8ebd8c1904
keywords:
- 面向连接的 NDIS WDK，重置 Nic
- CoNDIS WDK 网络、 重置 Nic
- 重置 NIC WDK 网络
- Nic WDK 网络、 重置
- 网络接口卡 WDK 网络、 重置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eae45af00de256eda41a1984cf195b0bee2cb0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379199"
---
# <a name="reset"></a>Reset





微型端口驱动程序或 MCM 驱动程序可能会调用 NDIS [ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)函数以重置 nic。

**请注意**  AF、 SAP 和 VC 句柄处于活动状态且在重置之前有效后重置处于活动状态且有效。

 

下图显示了客户端向微型端口驱动程序发出的重置请求。

![说明客户端向微型端口驱动程序发出的重置请求的关系图](images/cm-27.png)

下图显示了客户端到 MCM 驱动程序发出的重置请求。

![说明重置请求发出到 mcm 驱动程序的客户端的关系图](images/fig1-26.png)

当基础的面向连接的驱动程序正在重置 NIC 时，NDIS 通知每个绑定的协议通过调用的协议[ **ProtocolCoStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex)函数使用 NDIS\_状态\_重置\_开始。

重置的微型端口驱动程序或 MCM 驱动程序的 NIC 时，NDIS 将不会接受协议启动发送和微型端口驱动程序或 MCM 驱动程序的请求。 正在重置时，协议驱动程序不能尝试将数据包发送到的微型端口驱动程序与[ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)或来自与微型端口驱动程序请求信息[ **NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)。

*MiniportResetEx*执行任何依赖于设备的操作所需重置 NIC *MiniportResetEx*可以同步完成，或它可以通过调用以异步方式完成[ **NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismresetcomplete):

-   NDIS 如果重置完成同步后，调用每个绑定的协议*ProtocolCoStatusEx*函数和 NDIS\_状态\_重置\_结束。

-   NDIS 如果重置以异步方式完成，调用每个绑定的协议*ProtocolCoStatusEx*函数和 NDIS\_状态\_重置\_结束。

 

 





