---
title: 关闭 CoNDIS 呼叫管理程序或 MCM
description: 关闭 CoNDIS 呼叫管理程序或 MCM
ms.assetid: 6ef64e4c-eec4-4477-a06c-f80e21d5b1c7
keywords:
- 呼叫经理 WDK 网络，CoNDIS
- MCMs WDK 网络，关闭
- 微型端口呼叫管理器 WDK 网络，关闭
- 关闭呼叫管理器
- 关闭微型端口调用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ffbf6b59ce15212aa70272270f2107d0fe004ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838200"
---
# <a name="closing-a-condis-call-manager-or-mcm"></a>关闭 CoNDIS 呼叫管理程序或 MCM





当独立呼叫管理器从基础微型端口适配器取消绑定时，呼叫管理器必须通知受影响的所有 CoNDIS 客户端必须关闭关联的 AF。 为了通知每个客户端，NDIS 独立调用管理器调用[**NdisCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)函数。

如果 MCM 管理的 CoNDIS 微型端口适配器正在停止，则 MCM 必须通知所有受影响的客户端必须关闭关联的 AF。 为了通知每个客户端，MCMs 将调用[**NdisMCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)函数。

如果独立调用管理器或 MCM 分别调用**NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**，NDIS 将调用与相关联的 CoNDIS 客户端的[**ProtocolClNotifyCloseAf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_notify_close_af)函数。**NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**的*NdisAfHandle*参数中的句柄。 此调用会通知客户端关闭 AF。 如果**NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**返回 NDIS\_状态\_挂起，则在关闭时，ndis 将调用调用管理器的[**ProtocolCmNotifyCloseAfComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_notify_close_af_complete)函数通知操作已完成。

有关在 CoNDIS 客户端中关闭地址族的详细信息，请参阅[在 CoNDIS 客户端中关闭地址族](closing-an-address-family-in-a-condis-client.md)。

 

 





