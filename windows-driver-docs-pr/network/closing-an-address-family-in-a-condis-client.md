---
title: 关闭 CoNDIS 客户端中的地址系列
description: 关闭 CoNDIS 客户端中的地址系列
ms.assetid: 06e8128a-f3da-48f2-a045-6c4be5f85889
keywords:
- 客户端关闭 AFs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86c5e079fd2b4caa1ba4738f045b6ab1e948357e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384210"
---
# <a name="closing-an-address-family-in-a-condis-client"></a>关闭 CoNDIS 客户端中的地址系列





若要关闭 AFs，CoNDIS 客户端必须提供[ **ProtocolClNotifyCloseAf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_notify_close_af)函数。 NDIS 调用*ProtocolClNotifyCloseAf*当独立呼叫管理器或 MCM 调用[ **NdisCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)函数或[ **NdisMCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)函数，分别。

从内部*ProtocolClNotifyCloseAf*、 在客户端完成关闭指定的 AF，或返回 NDIS\_状态\_PENDING 和调用[ **NdisClNotifyCloseAddressFamilyComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclnotifycloseaddressfamilycomplete)函数来完成该操作。 客户端调用后**NdisClNotifyCloseAddressFamilyComplete**，NDIS 调用[ **ProtocolCmNotifyCloseAfComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_notify_close_af_complete)函数，以通知呼叫管理器，客户端关闭 AF。

若要关闭 AF，客户端应：

1.  如果客户端有活动的多点连接，调用[ **NdisClDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)函数根据需要多次，直到一个参与方将保持活动状态在每个 multipoint 虚拟连接 (VC)。

2.  调用[ **NdisClCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)函数，根据需要关闭的所有调用的仍是打开的都与的地址族。

3.  调用[ **NdisClDeregisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclderegistersap)函数根据需要取消注册的所有服务访问点 (SAPs) 与呼叫管理器注册了客户端的次数。

4.  调用[ **NdisClCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily)函数以关闭 AF。

 

 





