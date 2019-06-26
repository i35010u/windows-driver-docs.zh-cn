---
title: 关闭 CoNDIS 呼叫管理程序或 MCM
description: 关闭 CoNDIS 呼叫管理程序或 MCM
ms.assetid: 6ef64e4c-eec4-4477-a06c-f80e21d5b1c7
keywords:
- 调用的 CoNDIS-网络管理器 WDK
- MCMs WDK 网络关闭
- 微型端口调用管理器 WDK 网络关闭
- 结束调用管理器
- 关闭微型端口调用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0682b19b8f16426a27b267bcb2b049fd78b81101
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384221"
---
# <a name="closing-a-condis-call-manager-or-mcm"></a>关闭 CoNDIS 呼叫管理程序或 MCM





当独立呼叫管理器从基础的微型端口适配器取消绑定时，呼叫管理器必须通知所有受影响的 CoNDIS 客户端，它们必须关闭关联的 AF。 若要向每个客户端通知，NDIS 独立调用管理器调用[ **NdisCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)函数。

如果停止 MCM 管理的 CoNDIS 微型端口适配器，MCM 必须通知所有受影响的客户端，它们必须关闭关联的 AF。 向每个客户端，MCMs 调用通知[ **NdisMCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)函数。

如果调用独立呼叫管理器或 MCM **NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**分别 NDIS 调用[ **ProtocolClNotifyCloseAf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_notify_close_af)函数与在句柄关联的 CoNDIS 客户端*NdisAfHandle*参数的**NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**。 此调用会通知客户端关闭 AF。 如果**NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**返回 NDIS\_状态\_挂起、 NDIS 将调用在调用管理器的[**ProtocolCmNotifyCloseAfComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_notify_close_af_complete)时关闭通知操作已完成的功能。

有关关闭地址族的 CoNDIS 客户端中的详细信息，请参阅[关闭的 CoNDIS 客户端中的地址族](closing-an-address-family-in-a-condis-client.md)。

 

 





