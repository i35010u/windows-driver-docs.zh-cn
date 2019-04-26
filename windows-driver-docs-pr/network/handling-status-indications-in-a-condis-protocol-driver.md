---
title: 处理 CoNDIS 协议驱动程序中的状态指示
description: 处理 CoNDIS 协议驱动程序中的状态指示
ms.assetid: 948df51b-0561-4b67-b87f-e1652bb18772
keywords:
- 协议驱动程序 WDK 网络的 CoNDIS
- NDIS 协议驱动程序 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab0a234cf2f2e1f851d39b5827153b9c46b22766
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325709"
---
# <a name="handling-status-indications-in-a-condis-protocol-driver"></a>处理 CoNDIS 协议驱动程序中的状态指示





协议驱动程序必须提供[ **ProtocolCoStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570258) NDIS 调用时基础驱动程序将状态报告函数。

NDIS 调用协议驱动程序*ProtocolCoStatusEx*函数后基础驱动程序调用的状态指示函数 (例如， [ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)). 指示从微型端口驱动程序状态的详细信息，请参阅[CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)。

如果使用 OID 请求相关联的状态指示，则可以设置基础驱动程序**DestinationHandle**并**RequestId**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)以便 NDIS 可以提供的状态指示特定的协议绑定到包含状态信息的结构。 有关 OID 的请求的详细信息，请参阅[CoNDIS 协议驱动程序 OID 请求](condis-protocol-driver-oid-requests.md)。

 

 





