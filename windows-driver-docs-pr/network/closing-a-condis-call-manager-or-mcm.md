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
ms.openlocfilehash: ff88c1c9a61198e9207d24ae997df85238c32e53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338560"
---
# <a name="closing-a-condis-call-manager-or-mcm"></a>关闭 CoNDIS 呼叫管理程序或 MCM





当独立呼叫管理器从基础的微型端口适配器取消绑定时，呼叫管理器必须通知所有受影响的 CoNDIS 客户端，它们必须关闭关联的 AF。 若要向每个客户端通知，NDIS 独立调用管理器调用[ **NdisCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561680)函数。

如果停止 MCM 管理的 CoNDIS 微型端口适配器，MCM 必须通知所有受影响的客户端，它们必须关闭关联的 AF。 向每个客户端，MCMs 调用通知[ **NdisMCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff563546)函数。

如果调用独立呼叫管理器或 MCM **NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**分别 NDIS 调用[ **ProtocolClNotifyCloseAf** ](https://msdn.microsoft.com/library/windows/hardware/ff570234)函数与在句柄关联的 CoNDIS 客户端*NdisAfHandle*参数的**NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**。 此调用会通知客户端关闭 AF。 如果**NdisCmNotifyCloseAddressFamily**或**NdisMCmNotifyCloseAddressFamily**返回 NDIS\_状态\_挂起、 NDIS 将调用在调用管理器的[**ProtocolCmNotifyCloseAfComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570248)时关闭通知操作已完成的功能。

有关关闭地址族的 CoNDIS 客户端中的详细信息，请参阅[关闭的 CoNDIS 客户端中的地址族](closing-an-address-family-in-a-condis-client.md)。

 

 





